# methodl1. make fields red if is empty


   if (usernameTextField.text!.isEmpty || passwordTextField.text!.isEmpty || emailTextField.text!.isEmpty)
        {
            usernameTextField.attributedPlaceholder = NSAttributedString(string: "username", 
                            attribute: [NSForegroundColorAttributeName: UIColor.redColor()])
           
        }else{
            
        }
    }
    
    
#method 2. disable register button unless all fields are filled in.



       
