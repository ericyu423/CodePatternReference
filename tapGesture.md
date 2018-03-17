

# quickly turn any view in to a button

# make sure user Interaction is enable in code or at the storyboard
step. Declare UITapGestureReconizer a) give it a target b) direct it to a function

    UITapGestureRecognizer *tapGesture3 = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(bacCenterClicked)];
    [self.view addGestureRecognizer:tapGesture3];


