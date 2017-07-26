[Rocket](../Readme.md)/[tile](../tile.md)/[RocketTile](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/tile/RocketTile.scala)
========================


**********************

## case class RocketTileParams

~~~scala
case class RocketTileParams(
    core: RocketCoreParams = RocketCoreParams(),
    icache: Option[ICacheParams] = Some(ICacheParams()),
    dcache: Option[DCacheParams] = Some(DCacheParams()),
    rocc: Seq[RoCCParams] = Nil,
    btb: Option[BTBParams] = Some(BTBParams()),
    dataScratchpadBytes: Int = 0) extends TileParams
}
~~~

+ **core** `RocketCoreParams` (param) core parameter.
+ **icache** `Option[ICacheParams]` (param) instruction cache parameter (optional).
+ **dcache** `Option[DCacheParams]` (param) data cache parameter (optional).
+ **rocc** `Seq[RoCCParams]` (param) Rocket custom coprocessor parameters (optional).
+ **btb** `Option[BTBParams]` (param) branch target buffer parameter (optional).
+ **dataScratchpadBytes** `Int` (param) size of the scratch pad (conflict with D$).

## class RocketTile
*The Rocket tile generator (LazyModule).*

~~~scala
class RocketTile(val rocketParams: RocketTileParams, val hartid: Int)(implicit p: Parameters) extends BaseTile(rocketParams)(p)
    with HasExternalInterrupts
    with HasLazyRoCC  // implies CanHaveSharedFPU with CanHavePTW with HasHellaCache
    with CanHaveScratchpad // implies CanHavePTW with HasHellaCache with HasICacheFrontend
~~~

+ **rocketParams** `RocketTileParams` (param) parameter of the tile.
+ **hartid** `Int` the hardware thread identifier (identify a hard thread).
+ **module** `RocketTileModule(this)` pointer to the module implemenation.
+ **cpuDevice** `Device` the device decription for the processor.
  - reference: [Device node requirements](https://github.com/devicetree-org/devicetree-specification/blob/master/source/devicenodes.rst)
  - **reg** `Seq[ResourceInt]` address space of the tile (empty).
  - **device\_type** `Seq(ResourceString("cpu"))` a cpu device.
  - **compatible** `Seq(ResourceString("sifive,rocket0"), ResourceString("riscv"))` (manufacture,model)
  - **status** `Seq(ResourceString("okay"))` _okay_: CPU is running; _disabled_: CPU is in a quiecent state.
  - **clock-frequency** `Seq[ResourceInt]` current clock-frequency.
  - **riscv,isa** `Seq[ResourceString]` ISA description string.
  - **d-cache-block-size** `Seq[ResourceInt]` (optional) if use D$, size of a cache block in D$.
  - **d-cache-block-sets** `Seq[ResourceInt]` (optional) if use D$, number of sets in D$.
  - **d-cache-size** `Seq[ResourceInt]` (optional) if use D$, total size of D$ (sets \* ways \* block\_size)
  - **i-cache-block-size** `Seq[ResourceInt]` size of a cache block in I$.
  - **i-cache-block-sets** `Seq[ResourceInt]` number of sets in I$.
  - **i-cache-size** `Seq[ResourceInt]` total size of I$ (sets \* ways \* block\_size)
  - **next-level-cache** `Seq[ResourceReference]` (optional) reference to the outer level of cache/memory.
  - **tlb-split** `Unit` use split I-TLB and D-TLB.
  - **mmu-type** `Seq[ResourceString]` identify physical address width and page table levels. eg: "riscv,sv39"
  - **i-tlb-size** `Seq[ResourceInt]` (optional) number of TLB entries.
  - **i-tlb-sets** `Seq(ResourceInt(1))` (optional) number of sets. Always 1 as Rocket TLB is fully associative.
  - **d-tlb-size** `Seq[ResourceInt]` (optional) number of TLB entries.
  - **d-tlb-sets** `Seq(ResourceInt(1))` (optional) number of sets. Always 1 as Rocket TLB is fully associative.
  - **sifive,dtim** `Seq[ResourceReference]` refence to the SiFive data debug module.
  - **sifive,itim** `Seq[ResourceReference]` refence to the I$ frontend if SiFive instruction debug is enabled.

+ **intcDevice** `Device` the device description fo the interrupt controller.
  - **compatible** `Seq(ResourceString("riscv,cpu-intc"))`
  - **interrupt-controller**
  - **#interrupt-cells** `Seq(ResourceInt(1))`

+ **ResourceBinding** `=> Unit` register a resource binding function to the global BindingScope.<br>
  Currently it bind hartid to the cpu and interrupt controller in each tile.
  It also bind the interrupt controllers in tiles to the global PLIC according the interrupt interconnects.
  Obviously the registered binding functions will be called later in the compilation process in a lazy fashion.

## class RocketTileBundle
~~~scala
class RocketTileBundle(outer: RocketTile) extends BaseTileBundle(outer)
    with HasExternalInterruptsBundle
    with CanHaveScratchpadBundle
~~~

## class RocketTileModule
~~~scala
class RocketTileModule(outer: RocketTile) extends BaseTileModule(outer, () => new RocketTileBundle(outer))
    with HasExternalInterruptsModule
    with HasLazyRoCCModule
    with CanHaveScratchpadModule
~~~

+ **outer** `RocketTile` (param) pointer to the LazyModule.



<br><br><br><p align="right">
<sub>
Last updated: 26/07/2017<br>
[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com)<br>
[Apache 2.0](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.SiFive), &copy; (2016-2017) SiFive, Inc<br>
[BSD](https://github.com/freechipsproject/rocket-chip/blob/master/LICENSE.Berkeley), &copy; (2012-2014, 2016) The Regents of the University of California (Regents)
</sub>
</p>
