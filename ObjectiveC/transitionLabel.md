      code to make transition
      
      
         self.textViewDisplay.text = message1;
      

            [UIView transitionWithView:self.textViewDisplay
                      duration:0.4f
                       options:UIViewAnimationOptionTransitionCrossDissolve
                        animations:^{
                        
                        self.textViewDisplay.text = message2;
                        
           } completion:nil];


