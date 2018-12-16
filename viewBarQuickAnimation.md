quickly animate percentage bar

example.

storageBar is the container bar
greenView is the green bar that is going to grow.


CGRect rect = CGRectMake(_storageBar.frame.origin.x,
                              _storageBar.frame.origin.y,
                              0,
                              _storageBar.frame.size.height
                              );
    

    UIView *greenView = [[UIView alloc] initWithFrame:rect];
    greenView.backgroundColor=[UIColor greenColor];
    [self.view addSubview: greenView];
    
    
    
    [UIView animateKeyframesWithDuration:2.0
                                   delay:0.0
                                 options:UIViewAnimationOptionCurveEaseIn | UIViewAnimationOptionAllowUserInteraction
                              animations:^{
                                  
                                  greenView.frame = CGRectMake(_storageBar.frame.origin.x,
                                                               _storageBar.frame.origin.y,
                                                               _storageBar.frame.size.width * 0.75,
                                                               _storageBar.frame.size.height);
                                  
                              } completion:^(BOOL finished){
                                  
                              }];
