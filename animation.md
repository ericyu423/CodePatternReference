basically put all the pictures in an array and call it


 NSArray *imageNames = @[@"button_connecting_blink1", @"button_connecting_blink2"];
    NSMutableArray *images = [[NSMutableArray alloc] init];
    for (int i = 0; i < imageNames.count; i++) {
        [images addObject:[UIImage imageNamed:[imageNames objectAtIndex:i]]];
    }
    self.buttonImage.animationImages = images;
    self.buttonImage.animationDuration = 0.5;
    //animate image setup
    
    //animate battery image setup
    NSArray *imageNamesB = @[@"batt1",@"batt2",@"batt3",@"batt4",@"batt5",@"batt6",@"batt7",@"batt8",@"batt9",@"batt10",@"batt11"];
    NSMutableArray *imagesB = [[NSMutableArray alloc] init];
    for (int i = 0; i < imageNamesB.count; i++) {
        [imagesB addObject:[UIImage imageNamed:[imageNamesB objectAtIndex:i]]];
    }
    self.batteryImage.animationImages = imagesB;
    self.batteryImage.animationDuration = 2;
    
    
    
     if (ischarge)
    {
        [self.batteryImage startAnimating];
    }
    else
    {
        [self.batteryImage stopAnimating];
    }
