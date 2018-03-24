# step 1. create new proj following directions (download GoogleService-Info.plist), (add proj id)
# step 2. init pod, add 
        pod 'Firebase/Auth'
  	    pod 'Firebase/Database'
 	      pod 'Firebase/Storage'
# step 3* remeber to close the current proj, and open the white workspace 



    let email = "testing@hotmail.com"
        let password = "123123"
        Auth.auth().createUser(withEmail: email, password: password) { (user, error) in
            if let error = error {
                print("Failed to create user:",error)
            }
            
            print("Successfully created user:",user?.uid ?? "")
        }
    
