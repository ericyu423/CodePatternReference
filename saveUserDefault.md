


//dictionary array as an example


    if let myDict = UserDefaults.standard.value(forKey: "xyxzz") as? [String:String]{
            
            //user default access key is "xyxzz", if we find value come here
            
     }
     
     
     
     if var myDict = UserDefaults.standard.value(forKey: "xyxz") as? [String:String]{
            //append to dictionary and save it back
            myDict.updateValue("Hello",forKey: "key")
            UserDefaults.standard.set(myDict, forKey: "xyxz")
            
     }
