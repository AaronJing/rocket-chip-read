Class index
========================
***************************

+ AdapterNode<br>
  diplomacy.AdapterNode [class](../diplomacy/Nodes.md#class-adapternode)<br>
  diplomacy.IdentityNode [class](../diplomacy/Nodes.md#class-identitynode)<br>
  diplomacy.InputNode [class](../diplomacy/Nodes.md#class-inputnode)<br>
  diplomacy.MixedAdapterNode [class](../diplomacy/Nodes.md#class-mixedadapternode)<br>
  diplomacy.MixedNode [abstract class](../diplomacy/Nodes.md#abstract-class-mixednode)<br>
  diplomacy.NexusNode [class](../diplomacy/Nodes.md#class-nexusnode)<br>
  diplomacy.OutputNode [class](../diplomacy/Nodes.md#class-outputnode)<br>
  diplomacy.SinkNode [class](../diplomacy/Nodes.md#class-sinknode)<br>
  diplomacy.SourceNode [class](../diplomacy/Nodes.md#class-sourcenode)

+ ALU<br>
  rocket.ALU [class](../rocket/ALU.md#class-alu)

+ Arbiters<br>
  rocket.HellaCacheArbiter [class](../rocket/Arbiter.md#class-hellacachearbiter)<br>
  util.HellaCountingArbiter [class](../util/Arbiters.md#class-hellacountingarbiter)<br>
  util.HellaPeekingArbiter [class](../util/Arbiters.md#class-hellapeekingarbiter)<br>

+ Binding<br>
  diplomacy.Binding [case class](../diplomacy/Resources.md#case-class-binding)<br>
  diplomacy.BindingScope [trait](../diplomacy/Resources.md#trait-bindingscope); [object](../diplomacy/Resources.md#object-bindingscope)<br>

+ Blackbox<br>
  util.AsyncResetReg [class](../util/BackBoxRegs.md#class-asyncresetreg); [object](../util/BackBoxRegs.md#object-asyncresetreg)<br>
  util.AsyncResetRegVec [class](../util/BackBoxRegs.md#class-asyncresetregvec)<br>

+ Breakpoint<br>
  rocket.BPControl [class](../rocket/Breakpoint.md#class-bpcontrol)<br>
  rocket.BreakpointUnit [class](../rocket/Breakpoint.md#class-breakpointunit)

+ Clock<br>
  util.ClockDivider2 [class](../util/ClockDivider.md#class-clockdivider2)<br>
  util.Pow2ClockDivider [class](../util/ClockDivider.md#class-pow2clockdivider2)

+ Configs<br>
  rocketchip.BasePlatformConfig [class](../rocketchip/Configs.md#class-baseplatformconfig)

+ Counter<br>
  util.TwoWayCounter [object](../util/Counters.md#object-twowaycounter)<br>
  util.WideCounter [case class](../util/Counters.md#case-class-widecounter)

+ Crossing<br>
  util.AsyncBundle [final class](../util/AsyncBundle.md#final-class-asyncbundle)<br>
  util.AsyncQueue [class](../util/AsyncQueue.md#class-asyncqueue)<br>
  util.AsyncQueueSink [class](../util/AsyncQueue.md#class-asyncqueuesink)<br>
  util.AsyncQueueSource [class](../util/AsyncQueue.md#class-asyncqueuesource)<br>
  util.AsyncValidSync [class](../util/AsyncQueue.md#class-asyncvalidsync)<br>
  util.Crossing [abstract class](../util/Crossing.md#abstract-class-crossing)<br>
  util.CrossingIO [class](../util/Crossing.md#class-crossingio)<br>
  util.FromAsyncBundle [object](../util/AsyncBundle.md#object-fromasyncbundle)<br>
  util.GrayCounter [object](../util/AsyncQueue.md#object-graycounter)<br>
  util.ToAsyncBundle [object](../util/AsyncBundle.md#object-toasyncbundle)<br>
  util.UIntSyncChain [object](../util/AsyncQueue.md#object-uintsyncchain)<br>

+ Device<br>
  diplomacy.Description [case class](../diplomacy/Resources.md#case-class-description)<br>
  diplomacy.Device [abstract class](../diplomacy/Resources.md#abstract-class-device)<br>
  diplomacy.DeviceInterrupts [trait](../diplomacy/Resources.md#trait-deviceinterrupts)<br>
  diplomacy.DeviceRegName [trait](../diplomacy/Resources.md#trait-deviceregname)<br>
  diplomacy.MemoryDevice [class](../diplomacy/Resources.md#class-memorydevice)<br>
  diplomacy.SimpleDevice [class](../diplomacy/Resources.md#class-simpledevice)

+ DTS<br>
  diplomacy.DTS [object](../diplomacy.md/diplomacy/DeviceTree.md#object-dts)

+ Instruction<br>
  rocket.ExpandedInstruction [class](../rocket/RVC.md#class-expandedinstruction)<br>
  rocket.Instruction [class](../rocket/IBuf.md#class-instruction)

+ L1 cache<br>
  rocket.HasHellaCache [trait](../rocket/HellaCache.md#trait-hashellacache)<br>
  rocket.HasHellaCacheBundle [trait](../rocket/HellaCache.md#trait-hashellacachebundle)<br>
  rocket.HasHellaCacheModule [trait](../rocket/HellaCache.md#trait-hashellacachemodule)<br>
  rocket.HellaCache [class](../rocket/HellaCache.md#class-hellacache); [object](../rocket/HellaCache.md#object-hellacache)<br>
  rocket.HellaCacheBundle [class](../rocket/HellaCache.md#class-hellacachebundle)<br>
  rocket.HellaCacheIO [class](../rocket/HellaCache.md#class-hellacacheio)<br>
  rocket.HellaCacheModule [class](../rocket/HellaCache.md#class-hellacachemodule)<br>
  rocket.L1Metadata [class](../rocket/HellaCache.md#class-l1metadata)

+ L1 data cache<br>
  rocket.DCacheParams [case class](../rocket/HellaCache.md#case-class-dcacheparams)

+ L1 instruction cache<br>
  rocket.BHT [class](../rocket/BTB.md#class-bht)<br>
  rocket.BTB [class](../rocket/BTB.md#class-btb)
  rocket.RAS [class](../rocket/BTB.md#class-ras)

+ LazyModule<br>
  diplomacy.LazyModule [abstract class](../diplomacy/LazyModule/abstract-class-lazymodule); [object](../diplomacy/LazyModule/object-lazymodule)<br>
  diplomacy.LazyModuleImp [abstract class](../diplomacy/LazyModule/abstract-class-lazymoduleimp)

+ Node<br>
  diplomacy.BaseNode [abstract class](../diplomacy/Nodes.md#abstract-class-basenode)<br>
  diplomacy.BIND\_ONCE [case object](../diplomacy/Nodes.md#case-object-bind_once)<br>
  diplomacy.BIND\_QUERY [case object](../diplomacy/Nodes.md#case-object-bind_query)<br>
  diplomacy.BIND\_STAR [case object](../diplomacy/Nodes.md#case-object-bind_star)<br>
  diplomacy.InwardNode [trait](../diplomacy/Nodes.md#trait-inwardnode)<br>
  diplomacy.InwardNodeHandle [trait](../diplomacy/Nodes.md#trait-inwardnodehandle)<br>
  diplomacy.InwardNodeImp [trait](../diplomacy/Nodes.md#trait-inwardnodeimp)<br>
  diplomacy.NodeHandle [case class](../diplomacy/Nodes.md#case-class-nodehandle)<br>
  diplomacy.NodeImp [abstract class](../diplomacy/Nodes.md#abstract-class-nodeimp)<br>
  diplomacy.OutwardNode [trait](../diplomacy/Nodes.md#trait-outwardnode)<br>
  diplomacy.OutwardNodeHandle [trait](../diplomacy/Nodes.md#trait-outwardnodehandle)<br>
  diplomacy.OutwardNodeImp [trait](../diplomacy/Nodes.md#trait-outwardnodeimp)

+ Region<br>
  diplomacy.AddressRange [case class](../diplomacy/Parameters.md#case-class-addressrange); [object](../diplomacy/Parameters.md#object-addressrange)<br>
  diplomacy.AddressSet [case class](../diplomacy/Parameters.md#case-class-addressset); [object](../diplomacy/Parameters.md#object-addressset)<br>
  diplomacy.IdRange [case class](../diplomacy/Parameters.md#case-class-idrange)<br>
  diplomacy.RegionType [object](../diplomacy/Parameters.md#object-regiontype)<br>
  diplomacy.TransferSizes [case class](../diplomacy/Parameters.md#case-class-transfersizes)

+ RegisterCrossing<br>
  regmapper.BusyRegisterCrossing [class](../regmapper/RegisterCrossing.md#class-busyregistercrossing)<br>
  regmapper.RegisterWriteCrossing [class](../regmapper/RegisterCrossing.md#class-registerwritecrossing)

+ Resource<br>
  diplomacy.Resource [case class](../diplomacy/Resources.md#case-class-resource)<br>
  diplomacy.ResourceAddress [case class](../diplomacy/Resources.md#case-class-resourceaddress)<br>
  diplomacy.ResourceBinding [object](../diplomacy/Resources.md#object-resourcebindings)<br>
  diplomacy.ResourceBindings [case class](../diplomacy/Resources.md#case-class-resourcebindings)<br>
  diplomacy.ResourceInt [case class](../diplomacy/Resources.md#case-class-resourceint)<br>
  diplomacy.ResourceMapping [case class](../diplomacy/Resources.md#case-class-resourcemapping)<br>
  diplomacy.ResourceMap [case class](../diplomacy/Resources.md#case-class-resourcemap)<br>
  diplomacy.ResourceReference [case class](../diplomacy/Resources.md#case-class-resourcereference)<br>
  diplomacy.ResourceString [case class](../diplomacy/Resources.md#case-class-resourcestring)

+ RVC<br>
  rocket.IBuf [class](../rocket/IBuf.md#class-ibuf)
  rocket.RVCExpander [class](../rocket/RVC.md#class-rvcexpander)



<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 25/05/2017</sub></p>
