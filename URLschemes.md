# Callback to your app 

step 1. register plist


   <p align="center">
     <img src="https://github.com/ericyu423/CodePatternReference/blob/master/image/schemes.png" width="200"/>
   </p>

step 2. "myAppName://" this will get you back to your app

do something here you want. eg move to a view controller you want to goto


    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
          return true
    }
