# most used

              DispatchQueue.global().async {
                  //put in queue and go back to outer thread immedately do not wait
                  //basically tell you program to move the time consuming stuff away from main
              }
              
//this one is always inside some other block

              someBackgroundBlock {
                  DispatchQueue.main.sync {
                   //block thread untill I am done
                   //self.tableView.reloadData()  <-- reload data NOW 
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
      
      


