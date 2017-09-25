
//define toolbar

        private lazy var toolbar: UIToolbar = {
        let toolbar = UIToolbar()
        let item1 = UIBarButtonItem(title: "Cancel", style: UIBarButtonItemStyle.plain, target: self, action: #selector(cancel))
        
        let item2 = UIBarButtonItem(barButtonSystemItem: UIBarButtonSystemItem.flexibleSpace, target: self, action: nil)
        let item3 = UIBarButtonItem(title: "Done", style: UIBarButtonItemStyle.plain, target: self, action: #selector(done))
        toolbar.setItems([item1,item2,item3], animated: true)
        toolbar.tintColor = UIColor.white
        toolbar.barStyle = .blackTranslucent
        toolbar.sizeToFit()
        
        return toolbar
    }()
    
    @obj cancel(){}
    @obj done(){}
    
    
    _.inputView = timePicker (UIPicker)
    _.inputAccessoryView = toolbar
    
    
**important the picker will not clip to the toolbar so u need to make adjustment in storyboard
    
  autoreszing click the inner square
    
 default is L U R to the outer edge
 inner square only have horizontal <->  u also need to click on verticle
    
    
 <p align="center">
     <img src="https://github.com/ericyu423/MasterOneConceptPerDay/blob/master/image/resize.png" width="400"/>
 </p>
    
    
