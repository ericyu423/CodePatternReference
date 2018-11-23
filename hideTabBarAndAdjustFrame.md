when hide tabbar, viewcontroller will not adjust itself when it was first loaded
the following is a quick fix

 if (!self.tabBarController.tabBar.isHidden)
    {
        self.navigationController.view.frame =
        CGRectMake(self.navigationController.view.frame.origin.x, self.navigationController.view.frame.origin.y, self.navigationController.view.frame.size.width, self.navigationController.view.frame.size.height + 50);
        [self.navigationController.view setNeedsLayout];
        self.tabBarController.tabBar.hidden = YES;
        self.hidesBottomBarWhenPushed = NO;
    }
