# example 

# summary

closure made a copy of self, and that self point to the address of the class HTMELement
instance variable prapgrpah point to address of HTMELement 
same address in heap

so basically HTEMLement have reference count of 2

once paragraph = nil we still have a reference count of 1 of the instance variable 





        class HTMLElement {
            let name: String
            let text: String
            init(name: String, text: String){
                self.name = name
                self.text = text
            }

            lazy var asHTML: () -> String = { //lazy allow you to acess self
                [unowned self] in
                       print(Unmanaged.passUnretained(self).toOpaque())
                return "<\(self.name)>\(self.text)</\(self.name)>"
            }
            deinit {
                print("HTMLElement \(name) is being deallocated")
            }
        }

        var paragraph: HTMLElement? = HTMLElement(name: "p", text: "some sample paragraph body text")

        paragraph?.asHTML()

        //paragraph = nil
        print(Unmanaged.passUnretained(paragraph!).toOpaque())
        
        
        
        class HTMLElement {
    let name: String
    let text: String
    init(name: String, text: String){
        self.name = name
        self.text = text
    }
    
    lazy var asHTML: () -> String = { //lazy allow you to acess self
        [weak self] in
        guard let copyOfHTML = self else {return ""}
        
         print(Unmanaged.passUnretained(copyOfHTML).toOpaque())

              return "<\(copyOfHTML.name)>\(copyOfHTML.text)</\(copyOfHTML.name)>"
          }
          deinit {
              print("HTMLElement \(name) is being deallocated")
          }
      }

      var paragraph: HTMLElement? = HTMLElement(name: "p", text: "some sample paragraph body text")

      paragraph?.asHTML()

      //paragraph = nil
      print(Unmanaged.passUnretained(paragraph!).toOpaque())
