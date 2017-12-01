//example from interview


basically write the following function to an array extension

     func unique<T: Comparable>(array: Array<T>) -> Int {

            let sorted = array.sorted(by: <)
            let initial: (T?,Int) = (.none,0)

            //if things repeat don't add one
            let reduced = sorted.reduce(initial) { ($1, $0.0 == $1 ? $0.1 : $0.1 + 1)
            }
            return reduced.1
       }
       
* Step 1.
make sure you understand what the function does
1. <T: Comparable> (array: Array<T>) , this means this function will only take and array with 
elements that are comparable 
2. array.sorted(by: <) this sort the array from small to large
3. initial is tuple with type T optional and Int

* step2
once we fully understand what the fuction does is pretty easy
1. where Element: Comparable  , this just say we will only be able to appy to an array who have elementry that are sortable
2. "self" is the Array...for exame [4,3,2,3] <-- when you write this  this is an array and self is [4,3,2,3]
3. sorted is the sorted self

extension Array where Element: Comparable{
    func unique() -> Int {
        
        let sorted = self.sorted(by: <)
        let initial: (Element?,Int) = (.none,0)
        
        //if things repeat don't add one
        let reduced = sorted.reduce(initial) { ($1, $0.0 == $1 ? $0.1 : $0.1 + 1)
        }
        return reduced.1
    }
}

[1,2,3,4,5,5,6].unique()

   
