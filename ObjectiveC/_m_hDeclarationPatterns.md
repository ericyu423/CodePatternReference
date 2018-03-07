# Lazy initiation

          .m file
          
          @interface Deck()
          @property (strong, nonatomic) NSMutableArray *card;//I guess this is where you declare private properties
          @end
          @implementation Deck
          
          //this works like lazy in swift
          - (NSMutableArray *)cards
          {       //getter              = [[NSMutableArray alloc]init]; // work the same as new
                    if (!_cards) _cards = [NSMutableArray new];
                    return _card; //point at null adddress ,the above line will give it an address
          }
          
          


source https://stackoverflow.com/questions/13263229/objective-c-instance-variables


# Implementation with complete block. In older version is in Interface

          

          In  .m file
          @interface SomeClass ()<somethingDelegate>
          @end

          @implementation Someclass{
                    NSString *nsstringUnderInimplementation;
          };

          -(void)methodsAndSuch {}

          @end
          
          
          in .h
           @interface Someclass : NSObject {

                NSString *nsstringInInterface;

          }

          @end








source:https://stackoverflow.com/questions/2571518/class-variable-defined-at-implementation-rather-than-interface

SomeClass.h

          @interface Someclass : NSObject {

                NSString *nsstringInInterface;

          }

          @end

SomeClass.m

          @implementation Someclass

           NSString *nsstringUnderInimplementation;

          -(void)methodsAndSuch {}

          @end


in another file

    Someclass* firstObject = [Someclass new];
    Someclass* secondObject = [Someclass new];


    [firstObject setNsstringInInterface:@"A"];
    [secondObject setNsstringInInterface:@"B"];

    NSLog(@"%@",firstObject.nsstringInInterface);  // A  
    
    NSLog(@"%@",secondObject. sstringInInterface); // B
    
    //baisclaly instance variable, meaing they are different for every instance


    [firstObject setnsstringUnderInimplementation:@"A"];
    [secondObject setnsstringUnderInimplementation:@"B"];
    
NSLog(@"%@",[firstObject anotherExample]); //B
NSLog(@"%@",[secondObject anotherExample]); //B

//this is a global variable that is share by all instance

//Is like Swift Static class variable when doing OpenGL drawing triangles


*never declare an IBOutlet as a global var (in the implementation) if you are using it for localized nibs/xibs*
