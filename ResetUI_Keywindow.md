            
# keyWindow holds all the UI, keyWindow?.rootViewController is the root if set initially in appDelegate
            
            
            guard let mainTabBarController  = UIApplication.shared.keyWindow?.rootViewController as?
            MainTabBarViewController else {return}
            
            mainTabBarController.setupViewControllers()  //this reset the UI so when dimiss is called everything will be new
            self.dismiss(animated: true, completion: nil)
