
# how to use completion blocks in viewControllers

//if you call a viewController out of nowhere to do something and you want to dimisss it afterwards
//or notified some function to do something.

            import Foundation
            import UIKit

            class viewController: UIViewController {

                override func viewDidLoad() {
                    super.viewDidLoad()
                }

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
                    }
                }
            }


            class SecondViewController: UIViewController {


                override func viewDidLoad() {
                    super.viewDidLoad()
                }
                var completionBlock: (() -> ())?

                //meaning this will take a code block with no return value
                func doesSomething(){}
                func doesSomethingElse(){}

                func thisFunctionWillExecuteWhenThisViewControllerIsAboutToTerminate(){

                    completionBlock?()


                }
            }
            //cool extensions
            extension viewController {

                func controller(from storyboardName: String, name: String? = nil) -> UIViewController {
                    let storyboard = UIStoryboard(name: storyboardName, bundle: nil)
                    if let identifier = name {
                        return storyboard.instantiateViewController(withIdentifier: identifier)
                    }else{
                        return storyboard.instantiateInitialViewController()!
                    }
                }


            }
