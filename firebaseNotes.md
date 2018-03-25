//https://firebase.google.com/docs/reference/swift/firebasedatabase/api/reference/Classes/DatabaseReference


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
              
 # setValue replace everything under Users
 
            so if we write again using
            
            let value = [uid: ["username" : "eric"]
            Database.database().reference().child("users").setValue(value, withCompletionBlock: { (error, ref) in
                
                if let error = error {
                    print("failed to save user info to db",error)
                    return
                }
                
                print("Successfully saved user info to db")
                
              })//Database.database() ends
              
              
     we end up with     
     
            Users
             |----afioj2fopfa;wkdfjaks;dfj;kljafds
                            |-------- username : "eric"
                            
     the previous user and data and replace by the new structure
     
     
 # if we want update use updateChildValues(_:)
 
                users
                  |--  EouBZJGwYVRaWWinsq0bYSSlmgw2:1
                  |--  F4uk08QzWGe3mMQf4QAmDlKzCby2
                                |-----  username: "myNameIsEric"
                                
            
            let another = ["layer":"saveSomethingElse"]
            let dict = ["username":another]
            let value = [uid: dict]
            
            // this is to go to database  /users/ folder
            Database.database().reference().child("users").updateChildValues(value, withCompletionBlock: { (error, ref) in
                
                if let error = error {
                    print("failed to save user info to db",error)
                    return
                }
                
                print("Successfully saved user info to db")
            })//Database.database() ends
                
  Add another layer
  
                    
                users
                  |--  EouBZJGwYVRaWWinsq0bYSSlmgw2:1
                  |--  F4uk08QzWGe3mMQf4QAmDlKzCby2
                  |             |-----  username: "myNameIsEric"
                  |              
                  |--g5ErwMhgMKWvPmawzQ1RzviyKWl2
                                 |-----  username
                                            |-----  layer: "saveSomethingElse"

      
                
            
                             
# storage image and get image url (make sure to allow firebase storage first (database and storage are different) )

                Storage.storage().reference().child("profile_image").
                putData(uploadData, metadata: nil, completion: { (metadata, error) in
                
                if let error = error {
                    print("Failed to upload profil image:",error)
                    return
                }
                guard let profileImageUrl = metadata?.downloadURL()?.absoluteString else {return}
                
                print("Successfully uploaded profil image:",profileImageUrl)
            }) //storage().reference().child ends
            
            
  * metadata?.downloadURL()?.absoluteString  return s the url 
  * profile_image is put in storage with no folder structure right now
  
# storage image in a file structure

   add child("profile_images").child(filename)
   
   child basically = to  "/"  so we now have a  /profile_images/ folder
   inside the profile_image folder we have a file
   18EFEDA1-51D1-4A0D-A4C9-4B7DD836AB04 (uuid we generated which is our picture)
   
   so in firebase under storage we can click on profile_images, and it will open another page and show all the files
   that we saved
  
            
            
# connect Database and storage by storeing url to database

    Auth.auth().createUser(withEmail: email, password: password) { (user, error ) in
            if let error = error { print("Failed to create user:",error)}
            print("Successfully created user:",user?.uid ?? "")
            

            guard let image = self.photoButton.imageView?.image else { return }
            
            guard let uploadData = UIImageJPEGRepresentation(image, 0.3) else {return} //30% original
            let filename = UUID().uuidString
            Storage.storage().reference().child("profile_images").child(filename).putData(uploadData, metadata: nil, 
             completion: { (metadata, error) in
                
                if let error = error {
                    print("Failed to upload profil image:",error)
                    return
                }
                guard let profileImageUrl = metadata?.downloadURL()?.absoluteString else {return}
                print("Successfully uploaded profil image:",profileImageUrl)
                
                guard let uid = user?.uid else {return}
                let dictValues = ["username":username,"profileImageUrl": profileImageUrl]
                let value = [uid:dictValues]
                
                
                Database.database().reference().child("users").updateChildValues(value, withCompletionBlock: { (error, ref) in
                    
                    if let error = error {
                        print("failed to save user info to db",error)
                        return
                    }
                    
                    print("Successfully saved user info to db")
                    
                })//Database.database() ends

            }) //storage().reference().child ends
 
        }//Auth.auth().createUser ends
    
    }




        gBpaM41CZjSL9JMQP05ctZY6l2r1
            |---profileImageUrl: "https://firebasestorage.googleapis.com/v0/b/soc..."
            |----username: "Ericyu33"


# Get current user

        guard let uid = Auth.auth().currentUser?.uid else { return }
         
         Database.database().reference().child("users").child(uid).observeSingleEvent(of: .value, with: { (snapshot) in
            print(snapshot.value ?? "")
            
            guard let dictionary = snapshot.value as? [String: Any] else { return }
            
            let username = dictionary["username"] as? String
            self.navigationItem.title = username
            
        }) //observersingleEvent ends
        { (err) in
            print("Failed to fetch user:", err)
        }//closure ends
        
        
 this go to 
 database ----child-> users directory  ----child---->  uid (gBpaM41CZjSL9JMQP05ctZY6l2r1) 
 and get a snapshot it will be in key value pair
 
            
        gBpaM41CZjSL9JMQP05ctZY6l2r1
            |---profileImageUrl: "https://firebasestorage.googleapis.com/v0/b/soc..."
            |----username: "Ericyu33"
            
            
            
  dictionary will look like 

              po dictionary
            ▿ 2 elements
              ▿ 0 : 2 elements
                - key : "username"
                - value : Ericyu33
              ▿ 1 : 2 elements
                - key : "profileImageUrl"
                - value : https://firebasestorage.googleapis.com/v0/b/socialme.....
                
   let username = dictionary["username"] as? String 
   use key username to get the value Ericyu33



# Example fetching username and get the image  (2 step process)

                guard let uid = Auth.auth().currentUser?.uid else { return }
                        Database.database().reference().child("users").child(uid).observeSingleEvent(of: .value, with: { 
                        (snapshot) in  //.value = Any data changes at a location or, recursively, at any child node
                         
                            guard let dictionary = snapshot.value as? [String: Any] else { return }
                            self.user = User(dictionary: dictionary)
  
                        })  { (err) in
                            print("Failed to fetch user:", err)
                        }
                    }//fetchUser() ends
                    
                    
              user now have a username and a image url
              
take image URL and do the following to get image     


                        guard let profileImageUrl =  //get from the user truct else {return}
                        guard let url = URL(string: profileImageUrl) else { return }
                        URLSession.shared.dataTask(with: url) { (data, response, err) in
                            //check for the error, then construct the image using data
                            if let err = err {
                                print("Failed to fetch profile image:", err)
                                return
                            }
                            guard let data = data else { return }
                            let image = UIImage(data: data)

                            DispatchQueue.main.async {  //get back onto the main UI thread and update it
                                self.profileImageView.image = image  
                            }
                        }.resume()
                        
                        
                        
              
