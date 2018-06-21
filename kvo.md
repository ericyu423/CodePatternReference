

example 1.

        @objc class Person: NSObject {
            @objc dynamic var name = "old name"
        }
        let person = Person()

        person.observe(\Person.name, options: .old) { person, value in
            print("I am called \(person.name)")
            print("I was called \(String(describing: value.oldValue))")

        }
        person.name = "new name"
      
      
      
      
example 2.


          class CounterModel : NSObject {
              @objc dynamic var value = 10
              @objc dynamic var messages = [String]()
          }
          var model = CounterModel()

          model.observe(\CounterModel.value, options: [.initial]) { (model, change) in
              print("my value \(model.value)")
          }

          model.value = 11
          model.value = 12
          model.value = 13
          model.value = 16
          
          
          console:
          my value 10
          my value 11
          my value 12
          my value 13
          my value 16
