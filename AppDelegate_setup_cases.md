    
# With TabBarController or Regular UIViewController (With No Navigation Bar)

            func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
  
                window = UIWindow()
                let root = MainTabBarController()
                window?.rootViewController = root
                window?.makeKeyAndVisible()
                return true
            }
            
# Embed In Navigation Controller 

             func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

                  self.window = UIWindow(frame: UIScreen.main.bounds)
                  let navigationController = UINavigationController()
                  let mainView = MainViewController()
                  navigationController.viewControllers = [mainView]
                  self.window!.rootViewController = nav1
                  self.window?.makeKeyAndVisible()
                  return true
              } 


 
            
# Embed In Navigation Controller with context protocol
              //put in separate file Protocol.swift 
              import Foundation
              import CoreData
              protocol ContextProtocol {
                  func receiveContext(_ incomingContext: NSManagedObjectContext)
              }
 
              //AppDelegate.swift
              func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

                  self.window = UIWindow(frame: UIScreen.main.bounds)
                  let navigationController = UINavigationController()
                  let mainView = MainViewController()
                  mainView.receiveContext(self.persistentContainer.viewContext)
                  navigationController.viewControllers = [mainView]
                  self.window!.rootViewController = nav1
                  self.window?.makeKeyAndVisible()
                  return true
              } 
              
              //all subsequent views are added by following pattern
              //is a good idea to always use navigationController, you can always hide the bars if you don't like them
              let nextVC = SomeViewController()  //Name of your ViewController
              navigationController?.pushViewController(nextVC, animated: true)
              
              
#  StoryBoard Passing Context With Protocol

                //put in separate file Protocol.swift 
                import Foundation
                import CoreData
                 protocol ContextProtocol {
                    func receiveContext(_ incomingContext: NSManagedObjectContext)
                 }
            
            func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:     [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
  
                window = UIWindow()
                let main = MainViewController()
                mainView.receiveContext(self.persistentContainer.viewContext)
                window?.rootViewController = root
                window?.makeKeyAndVisible()
                return true
            }
              
