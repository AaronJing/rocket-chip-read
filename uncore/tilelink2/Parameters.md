[Rocket](../../Readme.md)/[uncore](../../uncore.md)/[tilelink2](../tilelink2.md)/[Parameters](https://github.com/ucb-bar/rocket-chip/blob/master/src/main/scala/uncore/tilelink2/Parameters.scala)
=====================

*TileLink2 interconnection parameters.*

**********************

### TL

Base TileLink connection.

### TLAsync

Asynchronous TileLink connection, cross asynchronous clock domains.

### TLRational

Mesochronous TileLink connection, cross source shared clock domains.


**********************

case class TLManagerParameters
------------
*Parameters for a TileLink2 manager.*

~~~scala
case class TLManagerParameters(
  address:            Seq[AddressSet],
  resources:          Seq[Resource] = Seq(),
  regionType:         RegionType.T  = RegionType.GET_EFFECTS,
  executable:         Boolean       = false, // processor can execute from this memory
  nodePath:           Seq[BaseNode] = Seq(),
  supportsAcquireT:   TransferSizes = TransferSizes.none,
  supportsAcquireB:   TransferSizes = TransferSizes.none,
  supportsArithmetic: TransferSizes = TransferSizes.none,
  supportsLogical:    TransferSizes = TransferSizes.none,
  supportsGet:        TransferSizes = TransferSizes.none,
  supportsPutFull:    TransferSizes = TransferSizes.none,
  supportsPutPartial: TransferSizes = TransferSizes.none,
  supportsHint:       TransferSizes = TransferSizes.none,
  fifoId:             Option[Int]   = None)
~~~

### Case variables:

+ **address**            `Seq[AddressSet]`

    Address range covered by this manager.

+ **resources**          `Seq[Resource] = Seq()`
+ **regionType**         `RegionType.T = RegionType.GET_EFFECTS`
+ **executable**         `Boolean = false`
+ **nodePath**           `Seq[BaseNode] = Seq()`
+ The supported types and sizes of packets
  + **supportsAcquireT**   `TransferSizes = TransferSizes.none`
  + **supportsAcquireB**   `TransferSizes = TransferSizes.none`
  + **supportsArithmetic** `TransferSizes = TransferSizes.none`
  + **supportsLogical**    `TransferSizes = TransferSizes.none`
  + **supportsGet**        `TransferSizes = TransferSizes.none`
  + **supportsPutFull**    `TransferSizes = TransferSizes.none`
  + **supportsPutPartial** `TransferSizes = TransferSizes.none`
  + **supportsHint**       `TransferSizes = TransferSizes.none`
+ **fifoId**             `Option[Int] = None`

### Member variables and functions:

+ **maxTransfer** `TransferSizes`

    The maximal packet size.

+ **maxAddress** `BigInt`

    The maximal address in all address spaces.

+ **name** `String`
+ **minAlignment** `BigInt`

    The minimal alignment of all address spaces.

+ **toResource** `_ => ResourceAddress`

    Convert this to `ResourceAddress`.

case class TLManagerPortParameters
--------------
*Parameters for a TileLink manager (upwards) port.*

~~~scala
case class TLManagerPortParameters(
  managers:   Seq[TLManagerParameters],
  beatBytes:  Int,
  endSinkId:  Int = 1,
  minLatency: Int = 0)
~~~

### Case variables:

+ **managers** `Seq[TLManagerParameters]`

    Parameters of the managers sharing this port.

+ **beatBytes** `Int`

    Number of bytes per beat.

+ **endSinkId** `Int = 1`
+ **minLatency** `Int = 0`

### Member variables and functions:

+ **maxTransfer** `_ => Int`

    The maximal packet size.

+ **maxAddress** `_ => BigInt`

    The maximal address in all address spaces.

+ Get the size of supported packets (the maximal size range supported by all managers)
  + **allSupportAcquireT**   `_ => TransferSizes`
  + **allSupportAcquireB**   `_ => TransferSizes`
  + **allSupportArithmetic** `_ => TransferSizes`
  + **allSupportLogical**    `_ => TransferSizes`
  + **allSupportGet**        `_ => TransferSizes`
  + **allSupportPutFull**    `_ => TransferSizes`
  + **allSupportPutPartial** `_ => TransferSizes`
  + **allSupportHint**       `_ => TransferSizes`

+ Get the supported types of packets (supported by any manager)
  + **anySupportAcquireT**   `_ => Boolean`
  + **anySupportAcquireB**   `_ => Boolean`
  + **anySupportArithmetic** `_ => Boolean`
  + **anySupportLogical**    `_ => Boolean`
  + **anySupportGet**        `_ => Boolean`
  + **anySupportPutFull**    `_ => Boolean`
  + **anySupportPutPartial** `_ => Boolean`
  + **anySupportHint**       `_ => Boolean`

+ Check whether an address is managed by this port with a certain type and size
  + **supportsAcquireTSafe**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsAcquireBSafe**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsArithmeticSafe** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsLogicalSafe**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsGetSafe**        `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutFullSafe**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutPartialSafe** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsHintSafe**       `(address: UInt, lgSize: UInt) => Bool`

+ Check whether an address is managed by this port with a certain type and size (fast version by assuming the address is valid)
  + **supportsAcquireTFast**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsAcquireBFast**   `(address: UInt, lgSize: UInt) => Bool`
  + **supportsArithmeticFast** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsLogicalFast**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsGetFast**        `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutFullFast**    `(address: UInt, lgSize: UInt) => Bool`
  + **supportsPutPartialFast** `(address: UInt, lgSize: UInt) => Bool`
  + **supportsHintFast**       `(address: UInt, lgSize: UInt) => Bool`

+ **routingMask** `BigInt`

    Which bits suffice to distinguish between all managers.

+ **find** `(address: BigInt) => Option[TLManagerParameters]`

    Get the `TLManagerParameters` of an address.

+ **findSafe** `(address: UInt) => Vec()`

    Return a bit vector that identifies the managers containing this address.

+ **containsSafe** `(address: UInt) => Bool`

    Whether this address is managed by this port.

+ **findFast** `(address: UInt) => Vec()`

    A faster version of `findSafe()` by assuming the address is valid.

+ **findFifoIdFast** `(address: UInt) => Int`

    Get the `fifoId + 1` or 0 if none.

+ **hasFifoIdFast** `(address: UInt) => Boolean`

    Whether there is a matched `fifoId`.


case class TLClientParameters
--------------
*Parameters for a TileLink client.*

~~~scala
case class TLClientParameters(
  sourceId:            IdRange       = IdRange(0,1),
  nodePath:            Seq[BaseNode] = Seq(),
  supportsProbe:       TransferSizes = TransferSizes.none,
  supportsArithmetic:  TransferSizes = TransferSizes.none,
  supportsLogical:     TransferSizes = TransferSizes.none,
  supportsGet:         TransferSizes = TransferSizes.none,
  supportsPutFull:     TransferSizes = TransferSizes.none,
  supportsPutPartial:  TransferSizes = TransferSizes.none,
  supportsHint:        TransferSizes = TransferSizes.none)
~~~

### Case variables:

+ **sourceId** `IdRange = IdRange(0,1)`

    Source ID range used for routing responses.

+ **nodePath** `Seq[BaseNode] = Seq()`
+ The supported types and sizes of packets
  + **supportsProbe**       `TransferSizes = TransferSizes.none`
  + **supportsArithmetic**  `TransferSizes = TransferSizes.none`
  + **supportsLogical**     `TransferSizes = TransferSizes.none`
  + **supportsGet**         `TransferSizes = TransferSizes.none`
  + **supportsPutFull**     `TransferSizes = TransferSizes.none`
  + **supportsPutPartial**  `TransferSizes = TransferSizes.none`
  + **supportsHint**        `TransferSizes = TransferSizes.none`

### Member variables and functions:

+ **maxTransfer** `TransferSizes`

    The maximal packet size.

+ **name** `String`

case class TLClientPortParameters
-----------------------
*Parameters for a TileLink client (downwards) port.*

~~~scala
case class TLClientPortParameters(
  clients:       Seq[TLClientParameters],
  unsafeAtomics: Boolean = false,
  minLatency:    Int = 0) // Atomics are executed as get+put
~~~

### Case variables:

+ **clients** `Seq[TLClientParameters]`

    Parameters of the clients sharing this port.

+ **unsafeAtomics** `Boolean = false`
+ **minLatency** `Int = 0`


### Member variables and functions:

+ **endSourceId** `_ => Int`

    The maximal source ID.

+ **maxTransfer** `_ => Int`

    The maximal packet size.

+ Get the size of supported packets (the maximal size range supported by all clients)
  + **allSupportProbe**      `_ => TransferSizes`
  + **allSupportArithmetic** `_ => TransferSizes`
  + **allSupportLogical**    `_ => TransferSizes`
  + **allSupportGet**        `_ => TransferSizes`
  + **allSupportPutFull**    `_ => TransferSizes`
  + **allSupportPutPartial** `_ => TransferSizes`
  + **allSupportHint**       `_ => TransferSizes`

+ Get the supported types of packets (supported by any client)
  + **anySupportProbe**      `_ => Boolean`
  + **anySupportArithmetic** `_ => Boolean`
  + **anySupportLogical**    `_ => Boolean`
  + **anySupportGet**        `_ => Boolean`
  + **anySupportPutFull**    `_ => Boolean`
  + **anySupportPutPartial** `_ => Boolean`
  + **anySupportHint**       `_ => Boolean`

+ Check for support of a given operation at a specific id
  + **supportsProbe**      `(id: UInt, lgSize: UInt) => Bool`
  + **supportsArithmetic** `(id: UInt, lgSize: UInt) => Bool`
  + **supportsLogical**    `(id: UInt, lgSize: UInt) => Bool`
  + **supportsGet**        `(id: UInt, lgSize: UInt) => Bool`
  + **supportsPutFull**    `(id: UInt, lgSize: UInt) => Bool`
  + **supportsPutPartial** `(id: UInt, lgSize: UInt) => Bool`
  + **supportsHint**       `(id: UInt, lgSize: UInt) => Bool`


+ **find** `(id: Int) => Option[TLClientParameters]`

    Get the `TLClientParameters` of an ID.

+ **find** `(id: UInt) => Vec()`

    Return a bit vector that identifies the clients.

+ **contains** `(id: UInt) => Bool`

    Whether this ID belongs to this port.

case class TLBundleParameters
------------------
*Parameters for a TileLink IO interface (Bundle).*

~~~scala
case class TLBundleParameters(
  addressBits: Int,
  dataBits:    Int,
  sourceBits:  Int,
  sinkBits:    Int,
  sizeBits:    Int)
~~~

### Case variables:

+ **addressBits** `Int`

    Size of address.

+ **dataBits**    `Int`

    Size of data.

+ **sourceBits**  `Int`

    Size of source ID.

+ **sinkBits**    `Int`

    Size of sink ID?

+ **sizeBits**    `Int`

    Size of size field.

### Member variables and functions:

+ **addrLoBits** `Int`

    Size of beat offset bits.

+ **union** `(x: TLBundleParameters) => TLBundleParameters`

    Return a parameter object that fits both `this` and `x`.

object TLBundleParameters
-------------------

+ **emptyBundleParams** `TLBundleParameters(1,8,1,1,1)`

    The default (empty) bundle parameter object.

+ **union** `(Seq[TLBundleParameters]) => TLBundleParameters`

    Get a parameter that fits all individual parameter objects.

+ **apply** `(TLClientPortParameters, TLManagerPortParameters) => TLBundleParameters`

    Generate a bundle parameter according to port parameters.

case class TLEdgeParameters
-------------
*Parameters for a TileLink connection.*

~~~scala
case class TLEdgeParameters(
  client:  TLClientPortParameters,
  manager: TLManagerPortParameters)
~~~

### Case variables:

+ **client** `TLClientPortParameters`

    Client side parameters.

+ **manager** `TLManagerPortParameters`

    Manager side parameters.

### Member variables and functions:

+ **maxTransfer** `Int`

    The maximal transfer size in both client/manager sides.

+ **maxLgSize** `log2Ceil(maxTransfer)`
+ **bundle** `TLBundleParameters(client, manager)`

case class TLAsyncManagerPortParameters
------------------
*Async TileLink (cross clock-domain) manager port parameters.*

~~~scala
case class TLAsyncManagerPortParameters(depth: Int, base: TLManagerPortParameters) { require (isPow2(depth)) }
~~~

case class TLAsyncClientPortParameters
------------------
*Async TileLink (cross clock-domain) client port parameters.*

~~~scala
case class TLAsyncClientPortParameters(base: TLClientPortParameters)
~~~

case class TLAsyncBundleParameters
-----------------
*Async TileLink (cross clock-domain) interface IO parameters.*

~~~scala
case class TLAsyncBundleParameters(depth: Int, base: TLBundleParameters)
~~~

+ **union** `(x: TLAsyncBundleParameters) => TLAsyncBundleParameters`

    Get a parameter that fits both `this` and `x`.

object TLAsyncBundleParameters
----------

+ **emptyBundleParams** `TLAsyncBundleParameters(1, TLBundleParameters.emptyBundleParams)`

    The default (empty) bundle parameter object.

+ **union** `(Seq[TLAsyncBundleParameters]) => TLAsyncBundleParameters`

    Get a parameter that fits all individual parameter objects.


case class TLAsyncEdgeParameters
------------
*Parameters for an asynchronous TileLink connection.*

~~~scala
case class TLAsyncEdgeParameters(
    client: TLAsyncClientPortParameters, manager: TLAsyncManagerPortParameters)
~~~

### Case variables:

+ **client** `TLAsyncClientPortParameters`

    Client side parameters.

+ **manager** `TLAsyncManagerPortParameters`

    Manager side parameters.

### Member variables and functions:

+ **bundle** `TLAsyncBundleParameters(client, manager)`




**********************

```scala
last_modified = 22/03/2017
authors       = Wei Song <wsong83@gmail.com>
license       = CC-BY <https://creativecommons.org/licenses/by/3.0/>
```
