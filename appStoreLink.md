

step1.   import StoreKit/and to link library

        blueProjectIcon -> select one of the targets (if multiiple add all) -> top tap (build Phases) -> linkbinarary
        



example code

                           add <SKStoreProductViewControllerDelegate> to VC


                          SKStoreProductViewController *storeVC = [ SKStoreProductViewController new];
                             
                             NSDictionary *parm = @{ SKStoreProductParameterITunesItemIdentifier : @"111111111111"};
                              storeVC.delegate = self;

                              [storeVC loadProductWithParameters:parm completionBlock:^(BOOL result, NSError *error)  {
                                  if (result) {
                                      //show
                                      
                                  }else {
                                      NSLog(@"ERROR WITH STORE CONTROLLER %@\n", error.description);
                                  }
                              }];



                            [self presentViewController:storeVC animated:YES completion:nil];


                                # use this to dimiss
                                - (void)productViewControllerDidFinish:(SKStoreProductViewController *)viewController {
                                    [viewController dismissViewControllerAnimated:YES completion:NULL];
                                }
