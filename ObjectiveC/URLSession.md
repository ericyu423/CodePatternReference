
# Configuration

     .default: Creates a default configuration object that uses the disk-persisted global cache, 
              credential and cookie storage objects.
     .ephemeral: Similar to the default configuration, except that all session-related data is 
                  stored in memory. Think of this as a “private” session.
     
         NOT WRITING ANYTHING TO DISK SO HAVE MORE PRIVACY   (SIZE LIMIT TO MEMORY)
         * When your app invalidates the session, all ephemeral session data is purged automatically. 
                  
     .background: Lets the session perform upload or download tasks in the background. 
                  Transfers continue even when the app itself is suspended or terminated by the system.
                  
# URLSessionTask                  

        URLSessionDataTask: for HTTP GET (retrieve data from servers to memory)
        
        URLSessionUploadTask:for HTTP POST or PUT method. (upload a file from disk to a web service)
        
        URLSessionDownloadTask: (download a file from a remote service to a temporary file location.)





# Code

        NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
                self.urlSession = [NSURLSession sessionWithConfiguration:configuration];

                NSURLSessionDataTask *dataTask = [self.urlSession dataTaskWithURL:url completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                    if (error != 0) {
                        NSLog(@"%@", error.description);
                    } else {
                        NSHTTPURLResponse *httpResponse = (NSHTTPURLResponse *)response;

                        if (httpResponse.statusCode == 200) {

                            NSLog(@"fetch successful");
                            NSMutableArray *users = [User parseJson:data];

                            dispatch_async(dispatch_get_main_queue(), ^{
                               success(nil, users);
                            });

                        } else {

                            NSLog(@"fetch was unsuccessful. code: %lu", httpResponse.statusCode);
                        }
                    }
                }];
                [dataTask resume];
            }
