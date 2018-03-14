

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
