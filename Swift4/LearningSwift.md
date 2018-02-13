
# capture list

        var a = 0
        var b = 0
        let Closure: () -> () = { [a,b] in
            print(a, b)
        }
        a=1
        b=2

        Closure()

this prints 0,0, we already capture (made copy of )a, b values 

# TODO: Still kind of confused about weak and unowned in closure come back to this later

# weak vs unowned
    //this one parentOf have a strong reference to self
    class Parent {
        var title = "Dad"
        lazy var parentOf:(String)->String = {
            (childname:String) in return childname+"'s "+self.title
        } 
    }
    
# unowned    
    class mParent {
        var title = "Dad"
        lazy var parentOf:(String)->String = {
            [unowned self] (childname:String) in return childname+"'s "+self.title
        } // OK
    }

# owned
    class Parent {
        var title:String? = "Dad"
        lazy var parentOf:(String)->String = {
            //title is not a class instance 
            [unowned self](childname:String) in return childname+"'s "+self.title!
        }
    }

# weak
    class Child {
        var parent:Parent?
        init (parent:Parent) {
            self.parent = parent
        }
        //parent is class instance so use weak
        lazy var myParent:()->() = { [weak parent = self.parent] in print(parent!.title) }
    }
