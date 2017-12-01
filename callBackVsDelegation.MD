# Delegation 

            protocol ServiceDelegate {
                func requestCompleted(result: String)
            }
          class Service {
              var delegate: NetworkServiceDelegate?

              func fetchDataFromUrl(url: String) {
                  url.request(.GET, url) { result in
                  
                      delegate?.requestComplete(result)
                  }
              }
          }
          class ViewController: UIViewController, ServiceDelegate {

              let service = NetworkService()

              override func viewDidLoad() {
                  super.viewDidLoad()
                  service.delegate = self
              }
              
              func requestCompleted(result: String) {
                  //code here get executed when request is complete
              }
          }
          
# callback example 1.  

                    class Service {

                         var completeBlock: ((result: String)->Void)?  //optional becauase the class
                         //might not be called by someone that provides you with with this code block

                        func fetchDataFromUrl(url: String) {
                           url.request(.GET, url) { result in
                                completeBlock?(result: result) 
      
                               }
                          }
                    }
                    
                  class ViewController: UIViewController {

                      let service = Service()

                      override func viewDidLoad() {
                          super.viewDidLoad()
                          service.CompleteBlock = { result in
                              //do stuff here
                          }
                      }
                  }
                  
 # callback in pratice example 2. 


        class viewController: UIViewController {
            func thisCallsViewController() {

                if let secondVC = controller(from: "storyboardName",name:"givenNameInStoryBoard") as? SecondViewController  {

                    secondVC.doesSomething()
                    secondVC.doesSomethingElse()
                    secondVC.completionBlock = {


                        //basically tell when other view controller need to do after is done
                        //such as notification, and dimiss vc

                      //  NotificationCenter.default.post(name: Notification.UserLogin , object: username)
                      //  self.dismiss(animated: false, completion: nil)

                    }
                    
                    option 1) call it straight up
                    present(secondVC, animated: true) // call the view controller, might need to call thea navigation stack vc 
                    and push on top of it do stuff once is completed
              
                    option 2) call nav controller push it on a stack or not if we use segue
                    let nav = UINavigationController(rootViewController: importController)
                    present(nav,animated: true)
                }
            }
        }


        class SecondViewController: UIViewController {
   
            var completionBlock: (() -> Void)?
            
      
            func doesSomething(){}
            func doesSomethingElse(){}

            func thisFunctionWillExecuteWhenThisViewControllerIsAboutToTerminate(){

                completionBlock?()


            }
        }
      
