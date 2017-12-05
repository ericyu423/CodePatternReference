after some experimenting with different syntaxes this works out.

note: making array of 3 elements with Array(repeating: UITextField, count: 3) doesn't work


        let textFields: [UITextField] = { fields in
        var textField = [UITextField]()
        for field in fields {
            var tf = UITextField()
            tf.placeholder = field
            tf.translatesAutoresizingMaskIntoConstraints = false
            tf.backgroundColor = UIColor(white: 0, alpha: 0.03)
            tf.borderStyle = .roundedRect
            tf.font = UIFont.preferredFont(forTextStyle: .body)
            textField.append(tf)
        }
         return textField
       }(["e-mail","username","password"])
       
       
       
