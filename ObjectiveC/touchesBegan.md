


        -(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
                [self.view endEditing:YES];

        }
        
        
Dismiss keyboard. This works because every view is a subclass of UIResponder, which it can response to user gestures
                  This will not work if there are views on top of this one. 
                  But i guess you can add endEditing to other subviews too.
