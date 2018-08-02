 objective C example

           UIAlertController *alert = [UIAlertController alertControllerWithTitle:@"Battery critically low!" message:@"\n\n\n\n\n" preferredStyle:UIAlertControllerStyleAlert];
              UIAlertAction *ok = [UIAlertAction actionWithTitle:@"OK" style:UIAlertActionStyleCancel handler:^(UIAlertAction * action) {
                  [self disconnectDevice];
                  [self deviceDisconnected:nil];
              }];

              UIImage *image = [UIImage imageNamed:@"LowBatteryAlert"];
              UIImageView *imageView = [[UIImageView alloc] initWithImage:image];

              [alert.view addSubview:imageView];

              imageView.translatesAutoresizingMaskIntoConstraints = NO;
           //these doesn't work
          //    [[imageView.leftAnchor constraintEqualToAnchor:alert.view.leftAnchor constant:0] setActive:YES];
          //    [[imageView.rightAnchor constraintEqualToAnchor:alert.view.rightAnchor constant:0] setActive:YES];
          //    [[imageView.centerXAnchor constraintEqualToAnchor:alert.view.centerXAnchor constant:0] setActive:YES];
          //       [[imageView.centerYAnchor constraintEqualToAnchor:alert.view.centerYAnchor constant:0] setActive:YES];

              [alert.view addConstraint:[NSLayoutConstraint constraintWithItem:imageView attribute:NSLayoutAttributeCenterX relatedBy:NSLayoutRelationEqual toItem:alert.view attribute:NSLayoutAttributeCenterX multiplier:1.0 constant:0.0]];
              [alert.view addConstraint:[NSLayoutConstraint constraintWithItem:imageView attribute:NSLayoutAttributeCenterY relatedBy:NSLayoutRelationEqual toItem:alert.view attribute:NSLayoutAttributeCenterY multiplier:1.0 constant:0.0]];
              [alert.view addConstraint:[NSLayoutConstraint constraintWithItem:imageView attribute: NSLayoutAttributeWidth relatedBy:NSLayoutRelationEqual toItem:nil attribute: NSLayoutAttributeNotAnAttribute multiplier:1.0 constant:230]];
              [alert.view addConstraint:[NSLayoutConstraint constraintWithItem:imageView attribute: NSLayoutAttributeHeight relatedBy:NSLayoutRelationEqual toItem:nil attribute: NSLayoutAttributeNotAnAttribute multiplier:1.0 constant:230 *(132.0/330.0)]];

              [alert addAction:ok];
              [self presentViewController:alert animated:YES completion:nil];


Swift Example:


      dismiss(animated: true, completion: {
            
            let numberOfBlankLines = 12
            let maxImageSize = CGSize(width: numberOfBlankLines * 16 , height: numberOfBlankLines * 16) //about 16 pt per return character
            let returnCharacters = String(repeating: "\n", count: numberOfBlankLines)
            let alertController = UIAlertController(title: "photo verification", message: msg + returnCharacters, preferredStyle: .alert)
            
            let imageView = UIImageView(image: image)
            
            let scaleSize = self.imageScaleSize(maxSize: maxImageSize ,image:image)
            
            alertController.view.addSubview(imageView)
            
            if (faceCount == 1){
                alertController.addAction(UIAlertAction(title: "Accepted", style: .default, handler: { _ in
                    self.performCheckin()
                }))
            }else{
                alertController.addAction(UIAlertAction(title: "Cancel", style: .cancel, handler: { _ in
                    //does nothing
                }))
                alertController.addAction(UIAlertAction(title: "Retry", style: .default, handler: { _ in
                    self.verifyUser()
                }))
            }
            
            //autolayout image to the center of alertView
            imageView.translatesAutoresizingMaskIntoConstraints = false
            alertController.view.addConstraint(NSLayoutConstraint(item: imageView, attribute: .centerX, relatedBy: .equal, toItem: alertController.view, attribute: .centerX, multiplier: 1, constant: 0))
            alertController.view.addConstraint(NSLayoutConstraint(item: imageView, attribute: .centerY, relatedBy: .equal, toItem: alertController.view, attribute: .centerY, multiplier: 1, constant: 0))
            alertController.view.addConstraint(NSLayoutConstraint(item: imageView, attribute: .width, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: scaleSize.width ))
            alertController.view.addConstraint(NSLayoutConstraint(item: imageView, attribute: .height, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: scaleSize.height ))
            
            self.present(alertController, animated: true, completion: nil)
        })//dimiss Alert completion ends
    
    
