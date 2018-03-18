
  # use postman to test end points quickly


# examle from work (POST)
    1. given url end point 
    2. login using POST
    

         1.
          given url.../user/login
          password = abc
          username = abc@hotmail.com

          2.  /user/login
          3. add parm in postman

          key
          password     abc
          username     abc@hotmail.com
          
          that is all pretty straight foward
          
          
          
          
          //in code
          //basically urlPath is the end point, dic is
          //NSDictionary *dic=@{@"username":self.userName.text,@"password":self.password.text};
          
                
          
           [session POST:urlPath parameters:dic progress:^(NSProgress * _Nonnull uploadProgress)
            {
         
            } success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
            
              } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
         
     
             }];
