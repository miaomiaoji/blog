@startuml
skinparam monochrome true 

object Object{
    prototype
}
object "Object Prototype" as Object_Prototype{
    constructor
    [[Prototype~]]
    —————————
    hasOwnPrototype()
    toString()
    isPrototypeOf()
}
object Person{
    prototype
}
object "Person Prototype" as Person_Prototype{
    constructor
     [[Prototype~]]
}
object person{
     [[Prototype~]]
}

Object -> Object_Prototype : prototype
Person -> Person_Prototype : prototype
Object <- Object_Prototype : constructor
Person <- Person_Prototype : constructor
Person_Prototype -up-> Object_Prototype : [[Prototype~]]
person -up-> Person_Prototype : [[Prototype~]]
center footer 原型链 
@enduml