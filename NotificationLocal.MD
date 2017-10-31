# Step1. Request Acess in AppDelegate

    import UserNotifications

    @UIApplicationMain
    class AppDelegate: UIResponder, UIApplicationDelegate,UNUserNotificationCenterDelegate {

        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {


            let center = UNUserNotificationCenter.current()
                center.delegate = self

                center.requestAuthorization(options: [.sound,.alert,.badge,.carPlay]) { (granted, error) in
                    if granted {
                        print("Notification Enable Successfully")
                    }else{
                        print("error")
                    }
                }

            return true

        }

        func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (_ options:UNNotificationPresentationOptions) -> Void)
        {
            print("\(notification.request.content.userInfo)")
        }

        //background
        func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response:UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void)
        {
            print("\(response.notification.request.content.userInfo)")
        }
    }
    
    
 # Set/Edit with Identifier (same Identifer will overwrite previous notification)
 
 
      @IBAction func setNewNotificationTime(_ sender: UIButton) {
      //click to overwrite
             SetUserNotification(identifier: "XSDIM",timeInterval: AlertTime.twentyFourHour)
        }
        
        override func viewDidLoad() {
            super.viewDidLoad()
            SetUserNotification(identifier: "XSDIM",timeInterval: AlertTime.fiveMinute)
        }



        func  SetUserNotification(identifier: String,timeInterval: AlertTime){
            let center = UNUserNotificationCenter.current()
            let content = UNMutableNotificationContent()
            content.title = "24 Hour till boarding"
            content.body = "it was set to alert in \(timeInterval.rawValue)"
            content.sound = UNNotificationSound.default()

            var trigger: UNTimeIntervalNotificationTrigger!

            trigger = UNTimeIntervalNotificationTrigger(timeInterval: timeInterval.rawValue, repeats: false)

            let request = UNNotificationRequest(identifier: identifier, content: content, trigger: trigger)
            center.add(request, withCompletionHandler: nil)

        }
        enum AlertTime:Double {
            case fiveMinute = 5
            case twentyFourHour = 50
        }
        
# Delete Notifications
 
     //you can pass in an array
     UNUserNotificationCenter.current().removePendingNotificationRequests(withIdentifiers: ["XSDIM"])
     
# UnitTest Find Current Pendings Notifcadtions

    UNUserNotificationCenter.current().getPendingNotificationRequests{ (pendingNotification) in 
            print("\(pendingNotification.count) 
            for notification in pendingNotification{
                print(notification.identifier)
          
            }
