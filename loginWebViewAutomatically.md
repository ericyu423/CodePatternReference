# Sent Javascript to webform
  email:
  password:
  [login button]
  
  we can sent javacript through webviewcontroller and get the form automatically filled
  
  look throught webpage source to make sure the corrent string are used for example
  in this case "login" doesn't work the webpage uses "loginForm"
  
  
          - (void)webViewDidFinishLoad:(UIWebView *)webView {
            NSString *savedUsername = @"ericyu423@hotmail.com";
            NSString *savedPassword = @"password1";

            if (savedUsername.length != 0 && savedPassword.length != 0) {
                //create js strings
                NSString *loadUsernameJS = [NSString stringWithFormat:@"var inputFields = document.querySelectorAll(\"input[type='email']\"); \
                                            for (var i = inputFields.length >>> 0; i--;) { inputFields[i].value = '%@';}", savedUsername];

                NSString *loadPasswordJS = [NSString stringWithFormat:@"var inputFields = document.querySelectorAll(\"input[type='password']\"); \
                                            for (var i = inputFields.length >>> 0; i--;) { inputFields[i].value = '%@';}", savedPassword];

               // [NSString stringWithFormat:@"document.forms["login"].submit();

                NSString *submitJS = [NSString stringWithFormat:@"document.forms[\"loginForm\"].submit();"];

                //autofill the form
                [self.webView stringByEvaluatingJavaScriptFromString: loadUsernameJS];
                [self.webView stringByEvaluatingJavaScriptFromString: loadPasswordJS];
                [self.webView stringByEvaluatingJavaScriptFromString: submitJS];
            }
        }
