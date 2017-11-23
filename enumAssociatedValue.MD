note:
when declared name(type,type....)
when acess 
    let .caseName(type, type...)
 or
         .caseName(let type,let type...)

        enum MyEnum {
            case x(Int, Int, Int)
            case y(Int, Int)
            case z(String)
        }

        var mypro = MyEnum.x(3,4,5)
         mypro = MyEnum.y(2,4)
         mypro = MyEnum.z("test")


        switch mypro {
        case let .x(a,b,c):
            print(a)
            print(b)
            print(c)

        case .y(let a,let b):
            print(a)
            print(b)
               // print("a: \(a) b: \(b)")
        case .z(let h):
                print(h)

        }
