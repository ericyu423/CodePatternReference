example objectC 


transition new view from button

        FurniturePickerViewController *vc = [[FurniturePickerViewController alloc] initWithNibName:@"FurniturePickerViewController" bundle:nil];
            vc.delegate = self;
            [self.view addSubview:vc.view];

            [self addChildViewController:vc];
            [vc.view layoutIfNeeded];


            CGRect rectViewOffScreen = CGRectMake(0,
                                                   self.view.bounds.size.height,
                                                   self.view.bounds.size.width,
                                                   self.view.bounds.size.height

                                                   );
            CGRect rectViewInScreen = CGRectMake( 0,
                                                  0,
                                                 self.view.bounds.size.width,
                                                 self.view.bounds.size.height);

            vc.view.frame = rectViewOffScreen;
            //line start
            [UIView animateWithDuration:0.3 animations:^{
                 vc.view.frame = rectViewInScreen;
            } completion:^(BOOL finished) {

            }];
            
            
Custom dimiss ObjectC

-(void)closeChildController{
    [UIView animateWithDuration:0.3 animations:^{
        
        self.view.frame = CGRectMake(
                0 ,
                super.view.frame.size.height,
                super.view.frame.size.width,
                super.view.frame.size.height);
        [self.view layoutIfNeeded];
    } completion:^(BOOL finished) {
        
        [self removeFromParentViewController];
    }];

}


custom dimiss Swift

  func closeChildController(){
        UIView.animate(withDuration: 0.3, animations: {
            () -> Void in
            
            self.view.frame = CGRect(x: 0, y: super.view.frame.size.height, width: super.view.frame.size.width,height: super.view.frame.size.height)
            self.view.layoutIfNeeded()
            
            //on iphone6.  before (0.0, 0.0, 375.0, 667.0) -> (187.5, 0.0, 375.0, 667.0)
            
            
            },
                       completion: { (true) -> Void in
                        self.removeFromParentViewController()
                        
        })
        
    }
    
