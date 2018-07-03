source: https://stackoverflow.com/questions/9011868/whats-the-best-way-to-detect-when-the-app-is-entering-the-background-for-my-vie

      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(appWillResignActive:) name:UIApplicationWillResignActiveNotification object:nil];
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(appWillTerminate:) name:UIApplicationWillTerminateNotification object:nil];
      
      
              -(void)appWillResignActive:(NSNotification*)note
              {

              }
              -(void)appWillTerminate:(NSNotification*)note
              {
                  [[NSNotificationCenter defaultCenter] removeObserver:self name:UIApplicationWillResignActiveNotification object:nil];
                  [[NSNotificationCenter defaultCenter] removeObserver:self name:UIApplicationWillTerminateNotification object:nil];

              }
              
              
              
 Swift
 
          override func viewDidLoad() {
            super.viewDidLoad()

            let app = UIApplication.shared

            //Register for the applicationWillResignActive anywhere in your app.
            NotificationCenter.default.addObserver(self, selector: #selector(ViewController.applicationWillResignActive(notification:)), name: NSNotification.Name.UIApplicationWillResignActive, object: app)
            }

            @objc func applicationWillResignActive(notification: NSNotification) {

            }
            
            
            
              init() {
              NotificationCenter.default.addObserver(self,
                                                     selector: #selector(applicationWillResignActive),
                                                     name: NSNotification.Name.UIApplicationWillResignActive,
                                                     object: nil)
              }

              deinit {
                  NotificationCenter.default.removeObserver(self,
                                                            name: NSNotification.Name.UIApplicationWillResignActive,
                                                            object: nil)
              }

              @objc private func applicationWillResignActive() {
                  self.header.blur.effect = nil
              }
