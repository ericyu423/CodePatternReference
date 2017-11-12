# Display short message to tell user something click ok to dismiss


# if is just a notice and does nothing else when ok is clicked

      //might be an idea to extend ViewController

        extension viewController {

             func showAlertMessage(title: String, message: String){
                let controller = UIAlertController(title: lString(title), message: lString(message), preferredStyle: .alert)
                controller.addAction(UIAlertAction(title: lString("Ok"), style: .default, handler: nil))
                present(controller, animated: true)

            }
        }


# if you need to do something about it


        let controller = UIAlertController(title: "title", message: "body", preferredStyle: .alert)
                   controller.addAction(UIAlertAction(title: "buttonTitle", style: .default, handler:{(Alert) in

                      //execute some code here when button is pressed


                   }))
        present(controller, animated: true)
  
# if you don't need the alert

      let controller = UIAlertController(title: "title", message: "body", preferredStyle: .alert)
                 controller.addAction(UIAlertAction(title: "buttonTitle", style: .default, handler:{_ in

                    //execute some code here when button is pressed


                 }))
      present(controller, animated: true)
