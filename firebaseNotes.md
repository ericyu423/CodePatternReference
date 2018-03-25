# step 1. create new proj following directions (download GoogleService-Info.plist), (add proj id)
# step 2. init pod, add 

    pod 'Firebase/Auth'
  	pod 'Firebase/Database'
 	pod 'Firebase/Storage'
        
# step 3a remeber to close the current proj, and open the white workspace 
# step 4. follow directions from firebase webpage, add FirebaseApp.configure() in app delegate, import firebase

    let email = "testing@hotmail.com"
        let password = "123123"
        Auth.auth().createUser(withEmail: email, password: password) { (user, error) in
            if let error = error {
                print("Failed to create user:",error)
            }
            
            print("Successfully created user:",user?.uid ?? "")
        }
        
        if email or password is missing error will actually tell you
        
        
# step5. go back to firebase console (webpage) enable email authentication  

    discover firebase -> Authentication(get started) -> Setup sign in method ->
    
    enable email
    
    (look like we also have option to sign up with phone, goolge, facebook, twitter ..ect)
    
# step6. 
        Authentication user tap can see registered users.
        error will show if user try to register with same email twice.
        
        
    


# write stuff to database

the database have a structure of

Databasename (whatever you name your project)
        Users  (user directory to save data for a particular user)
        
        
to write user we can use userid as a key (id from registration)        



            let value = [uid: 1]  //userID = EauBZjGwYVRaWWknsq0bYSSlmgw1

            
            // this is to go to database  /users/ folder
            Database.database().reference().child("users").setValue(value, withCompletionBlock: { (error, ref) in
                
                if let error = error {
                    print("failed to save user info to db",error)
                    return
                }
                
                print("Successfully saved user info to db")
                
              })//Database.database() ends
        
  we end up with
           
           Users
              |----- EauBZjGwYVRaWWknsq0bYSSlmgw1:1
