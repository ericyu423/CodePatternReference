# sync vs async

# stiuation 1.    excute all step one things before moving to step 2

            DispatchQueue.global(qos: .background).sync { 
                   for _ in 1...10 { 
                          print(“step1”) 
                   } 
            } 
            for _ in 1...3 { 
                   print(“step2”) 
            } 
            
  this print 1,1,1,1,1,1,1,1,1,1,2,2,2,2,2,2,2,2,2,2,2 
 
            when change to .aync
            
           2,1,2,1,2,2,2,2,2,2,2,2,1,1,1,1,1,1,1,
           
           
# download multiple thing in the back ground
            let x = DispatchQueue(label: "x")
            let y = DispatchQueue(label: "y")


             x.async { for _ in 1...10 { print("1") } }
             y.async { for _ in 1...10 { print("2") } }

             for _ in 1...10 { print("3") }
             
             2331232112321213....mix together
     
# download iamge display but dont' freeze the UI

            DispatchQueue.global(qos: .background).async {
            
                        imageManger.requestImage{
    
                                   // for chekcing
                                    DispatchQueue.main.async {
                                          //this is UI
                                    self.collectionView?.reloadData()
                                     }
                        }
            }


# UI example

AppDelegate -> tabBarController  

      if we present a login viewcontroller in view did load, because tabbarController is not done loading
      we get a view hierarchy error
      
      class MainTabBarViewController: UITabBarController {

     override func viewDidLoad() {
        super.viewDidLoad()
        
         if Auth.auth().currentUser == nil {
            DispatchQueue.main.async {
            let loginVC = LoginViewController()
            self.present(loginVC, animated: true, completion: nil)
            }
        }
        
so we wait till tabbarController finish setup in UI by using DispatchQueue.main.async


          Asynchronous function returns control on the current queue right after task 
          has been sent to be performed on the different queue. It doesn't wait until 
          the task is finished. It doesn't block the queue.
        
        
   Summary: with Async presnet(loginVC) will not block your initialization of TabBarControllers     
