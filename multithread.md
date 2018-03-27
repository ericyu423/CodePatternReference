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
