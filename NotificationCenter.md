

      extension Notification.Name {
          static let MyCustomNotification = Notification.Name("MyCustom")
      }



    viewDidLoad (  //if you don't put in the object for sytem notification nothing will happen)
    
         NotificationCenter.default.addObserver(self, selector: #selector(textDidChange(_:)), name: Notification.Name.UITextFieldTextDidChange, object: textfield)
        
         NotificationCenter.default.addObserver(self, selector: #selector(textStartEdit(_:)), name: Notification.Name.UITextFieldTextDidBeginEditing, object: textfield)
       
         NotificationCenter.default.addObserver(self, selector: #selector(seqControl(_:)), name: Notification.Name.MyCustomNotification, object: nil)
         
         

        @IBAction func SegmentControlDidChange(_ sender: UISegmentedControl) {
            //sent out (post) notification whoever is lisenting to it will respond
            NotificationCenter.default.post(name: Notification.Name.MyCustomNotification, object: nil)
        }

        @objc func seqControl(_ notification: Notification){
            mylabel.text = "got here with custom notification"  // Notification.Name.MyCustomNotification calls seqControl
        }
        @objc func textDidChange(_ notification: Notification){ //default notification, keyboard one is used a lot
            mylabel.text =  "text did change bring me here"
        }

        @objc func textStartEdit(_ notification: Notification){
            mylabel.text =  "text become First Responder"
        }
