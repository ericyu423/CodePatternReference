# most used

              DispatchQueue.global().async {
                  //put in queue and go back to outer thread immedately do not wait
                  //basically tell you program to move the time consuming stuff away from main
              }
              
//example

              someBackgroundBlock {
                  DispatchQueue.main.sync {
                   //block thread untill I am done
                   //self.tableView.reloadData()  
                  }
              }
              
              
//example              

            let session = URLSession(configuration: .default)
            if let url = URL(string: "http://") {
                let task = session.dataTask(with:url) {(data: Data?, reponse, error) in
                
                print("do other stuff")
                
                    DispatchQueue.main.async{

                    }
                    print("do stuff")
                }
                task.resume()
            }
            print("I am outside the block")
            
step 1. no stopping all step happens immediately
  created urlsession, task and task.resume() sent it to another thread to run the block prints " I am outside the block"
  
step 2. "do stuff" might take a while only after you get the data, you might not care about the info
        "do stuff with UI" happen immediately after fnishing with main.aync
        than finally do thing inside main.async
        
        
example 2:     

            private func fetchImage(){
                if let url = imageURL { [weak self] in

                    DispatchQueue.global(qos: .userInitiated).async {
                        if let imageData = urlContents, url == self?.imageUrl{

                            DispatchQueue.main.async {
                                self?.image = UIImage(data: imageData)
                            }

                        }

                    }
                }
            }
        



# Quickest - .main   (short and quick,high priority)
    
      let main = .main                    
        
# Global - .global()   (speed from fast to slow as described in the desciprtion inside qaulity of service)

    //full name "DispatchQoS.userInteractive"

    let background1 = .global(qos: .userInteractive)  //almost as fast as main, like keeping track of the finger motion
    let background2 = .global(qos: .userInitiated)
    let background3 = .global(qos: .background)
    let background3 = .global(qos: .utility)
    
# Customer - Serial: DispatchQueue(label: "I will show up in debugger") 
# Customer - Concurrent: Dispatch(label: "I will show up in debugger", attributes: .concurrent)

# async modifier

we almost always use this one ASYNC, Does nothing except put it in queue

**************************************************************
             backgroundQueue1.async {
                          //code
              }
**************************************************************

This is like getting the ticket number at DMV, once you get the ticket your in line
but you don't know when is your turn


# sync modifer - the operation or activity of two or more things at the same time or rate 

we will NEVER do this in main queue (because it freeze User interface)

**************************************************************
      background1.sync { 
            for _ in 1...100 { print("Do Now") }
      }
      print("Do After")
**************************************************************
      after printing "Do Now" 100x it will print "Do After"
      
      


