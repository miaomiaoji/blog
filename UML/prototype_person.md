@startuml
skinparam monochrome true 

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

Person -> Person_Prototype : prototype
Person <- Person_Prototype : constructor
person -up-> Person_Prototype : [[Prototype~]]

center footer 构造函数、原型对象和实例
@enduml