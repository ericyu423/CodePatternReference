

# coversation looking modal view


most important thing is remeber to set this property

          func adaptivePresentationStyleForPresentationController(controller: UIPresentationController!) -> UIModalPresentationStyle {

              return .None
          }


in objective C

          -(UIModalPresentationStyle)adaptivePresentationStyleForPresentationController:(UIPresentationController *)controller
          {
              return UIModalPresentationNone;
          }
          
          
without this iphone will show full page popover


# example from work

                              //drawLinepopover is a viewcontroller that is setup in .m file with layouts in xib

                         self.drawLinePopoverView = [[DrawLinePopoverViewController alloc] init];

                        self.drawLinePopoverView.name = @"test";
                        self.drawLinePopoverView.des = @"some message";
                        self.drawLinePopoverView.preferredContentSize = CGSizeMake(180, 120); //size of popover
                        self.drawLinePopoverView.modalPresentationStyle = UIModalPresentationPopover;
                        [self prepareInfoCheckPopoverControllerWithVC:self.drawLinePopoverView forPoint: CGPointMake(180, 120) ]; //draw it some point...or use view.center of some view
                        [self presentViewController:self.drawLinePopoverView animated:YES completion:nil];
