use SafeAreaLayoutGuide instead of bottom anchor, or your view will be slightly lower than the edge of the iphone

  if (@available(iOS 11.0, *)) {
        [[self.webView.safeAreaLayoutGuide.topAnchor constraintEqualToAnchor:self.view.bottomAnchor constant:-50] setActive:true];
    } else {
       [[self.webView.bottomAnchor constraintEqualToAnchor:self.view.bottomAnchor constant:-200] setActive:true];
    }
    
   
