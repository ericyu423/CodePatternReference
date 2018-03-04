- Journey to be a more effcient programmer

2-1-2018 - 3-1-2018 (Objective-C)

What did I learn this month.

From online lectures and reading.

1. In-depth understanding of Reference Counting. Strong reference cycle
    Basically having instance pointing to eachother in a heap will cause a problem of strong reference cycle
    since ARC track all pointers, however a weak pointer is not tracked so, when the object loses all strong reference
    to itselft it will get deleted.
    
2. In-depth understadning of MVC design pattern

    View uses delegate, datasource and target action to talk to the controller (UIViewController)
    When model is updated it can using Notifications to talk to Controller
    
    
    given a controllerA with a view that have a controllerB
    controlerA should treat controllerB as if it was a view. i.e. use delegate to talk about or completion block.
    
    
    
From working.

1.  xib is created at the same time when new file is created
2. reuseable cell can have an xib which might look a bit more clearer rather than put everything in one storyboard VC
3. properties.
4. It make debugging easier if you know certain functions are private. 
5. Make a graph of VC and subview vc it will save time down the road
6. mutiple releases to testflight, with mutiple version of your app that can be run on testflight is easier to debug if new feature breaks the existing function




