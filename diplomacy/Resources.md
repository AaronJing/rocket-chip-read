[Rocket](../Readme.md)/[diplomacy](../diplomacy.md)/[Resources](https://github.com/freechipsproject/rocket-chip/blob/master/src/main/scala/diplomacy/Resources.scala)
=====================

*Device tree generation helpers*

**********************

case class ResourceAddress(address: Seq[AddressSet], r: Boolean, w: Boolean, x: Boolean)
-----------------
```scala
final case class ResourceAddress(address: Seq[AddressSet], r: Boolean, w: Boolean, x: Boolean)
    extends ResourceValue
```

*An address space with permission bits.*

+ **address** `Seq[AddressSet]` address space.
+ **r** `Boolean` readable.
+ **w** `Boolean` writable.
+ **x** `Boolean` executable.

case class ResourceMapping(address: Seq[AddressSet], offset: BigInt)
-----------------------
```scala
final case class ResourceMapping(address: Seq[AddressSet], offset: BigInt) extends ResourceValue
```


case class ResourceInt(value: BigInt)
-----------------------
```scala
final case class ResourceInt(value: BigInt) extends ResourceValue
```

case class ResourceString(value: String)
-----------------------
```scala
final case class ResourceString(value: String) extends ResourceValue
```

case class ResourceReference(value: String)
-----------------------
```scala
final case class ResourceReference(value: String) extends ResourceValue
```

case class ResourceMap(value: Map[String, Seq[ResourceValue]], labels: Seq[String])
-----------------------
```scala
final case class ResourceMap(value: Map[String, Seq[ResourceValue]], labels: Seq[String] = Nil)
    extends ResourceValue
```

case class Binding(device: Option[Device], value: ResourceValue)
----------------------
*Bind a device to a resource configuration. If device is None, the value is global.*


case class ResourceBindings(map: Map[String, Seq[Binding]])
----------------------
*A map of resource bindings.*

+ **apply** `(key: String) => Seq[Binding]`

    Get the bindings of ("int").

case class Description(name: String, mapping: Map[String, Seq[ResourceValue]])
----------------------
*The discription of a device. Serialization friendly?*

abstract class Device
-----------------------
*Definition of a device*

+ **describe** `(resources: ResourceBindings) => Description`

    Generate the device description.

+ **label** `String` A unique label of a device.

trait DeviceInterrupts
-----------------------
*Interrupts of a device (extensible only to Device).*

+ **alwaysExtended** `Boolean = false`

    Not a concrete device (but a middle layer agent)??

+ **describeInterrupts** `(resources: ResourceBindings) => Map[String, Seq[ResourceValue]]`

    return interrupt definitions.

  + `("interrupt-parent" -> Seq(ResourceReference(Device.label)))` A concrete device's label.
  + `("interrupts" -> Seq[ResourceValue])` A concrete device's interrupts.
  + `("interrupts-extended" -> Seq[ResourceMap])` An extended devices' interrupts.

+ **int** `_ => Seq(Resource(this, "int"))`

    ??

trait DeviceRegName
-------------------------
*Device registration name (extensible only to Device).*

+ **prefix** `String = "soc/"*` prefix
+ **describeName** `(devname: String, resources: ResourceBindings) => String`

    Get the device name string. For a valid device, the name is `$prefix/$devname@$base_addr`

+ **reg** `_ => Seq(Resource(this, "reg"))`

    ??

class SimpleDevice(devname: String, devcompat: Seq[String])
-------------------
```scala
class SimpleDevice(devname: String, devcompat: Seq[String])
    extends Device with DeviceInterrupts with DeviceRegName
```

*Simple device device definition.*

+ *describe: (resources: ResourceBindings) => Description*: generate a description of this device
```scala
Description(describeName(devname, resources),
    ListMap("reg"        -> resources("reg").map(_.value),
            "compatible" -> devcompat.map(ResourceString(_)), // optional
            describeInterrupts(resources)))
```

class MemoryDevice
-----------------------
```scala
class MemoryDevice extends Device with DeviceRegName
```

*Simple memory device definition*

+ override prefix to "".
+ *describe: (resources: ResourceBindings) =>  Description*: generate a description of this device
```scala
Description(describeName("memory", resources),
    ListMap("reg"         ->resources("reg").map(_.value),
            "device_type" -> Seq(ResourceString("memory"))))
```


case class Resource(owner: Device, key: String)
----------

+ **bind** `(user: Device, value: ResourceValue) => Unit`
+ **bind** `(value: ResourceValue) => Unit`

trait BindingScope
-----------
*(extensible only to LazyModule)*

+ **bindingTree** `_ => ResourceMap`

    Generate device tree map.

object BindingScope
------------
+ **active** `Option[BindingScope]`

    The current active LazyModule needing binding.

+ **find** `(m: Option[LazyModule]) => Option[BindingScope]`

    Return the first parent `LazyModule` extended with `BindingScope`.

object ResourceBinding
-------------
*An global function object that is called with extension (weird Scala code pattern) in a device to initialize all binding functions.*

+ **apply** `(block: => Unit): Unit`

    Add a new code segement `block` into the binding functions.


<br><br><br><p align="right"><sub>[CC-BY](https://creativecommons.org/licenses/by/3.0/), &copy; (2017) [Wei Song](mailto:wsong83@gmail.com), 13/03/2017</sub></p>

