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
