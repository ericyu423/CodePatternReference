# continue fire background Timer when screen is off or app in background mode 

          appdelegate.m

          - (void)applicationDidEnterBackground:(UIApplication *)application {

              UIBackgroundTaskIdentifier bgTask =0;
              UIApplication  *app = [UIApplication sharedApplication];
              bgTask = [app beginBackgroundTaskWithExpirationHandler:^{
                  [app endBackgroundTask:bgTask];
              }]; 

          }
          
          
          
some where in the file 

           
                self.powerSaverTimer = [[NSTimer alloc] initWithFireDate:[NSDate dateWithTimeIntervalSinceNow:5] interval:10 repeats:YES block:^(NSTimer * _Nonnull timer) {
                    if(self.powerSaverExtendCount == 50) {
                        [self.powerSaverTimer invalidate];
                        self.powerSaverTimer = nil;
                        NSLog(@"Reach 2 times power saver extends, stop");
                        return;
                    }
                    NSLog(@"Fire power save timer once!");
                    [self.currentDevice getMeasureCount];
                    self.powerSaverExtendCount += 1;

                }];
                NSRunLoop *runLoop = [NSRunLoop currentRunLoop];
                [runLoop addTimer:self.powerSaverTimer forMode:NSDefaultRunLoopMode];
      
 
    // [self.currentDevice getMeasureCount]; continue to update every 10 sec
