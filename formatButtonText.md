
# print out "Don't have an account Sign Up" where Sign Up is blue and bold



         let attributedTitle = NSMutableAttributedString(string: "Don't have an account ",
                                                        attributes: 
                                                        [NSAttributedStringKey.font: UIFont.systemFont(ofSize: 14), 
                                                         NSAttributedStringKey.foregroundColor: UIColor.lightGray])
     
        
        attributedTitle.append(NSMutableAttributedString(string: "Sign Up", 
                                                      attributes:
                                                      [NSAttributedStringKey.font: UIFont.boldSystemFont(ofSize: 14),
                                                       NSAttributedStringKey.foregroundColor: 
                                                            UIColor(red: 17/255, green: 154/255, blue: 237/255, alpha: 1)
            ]))
        
        
         //UIColor.rgb(red: 17, green: 154, blue: 237)
          button.setAttributedTitle(attributedTitle, for: .normal)
