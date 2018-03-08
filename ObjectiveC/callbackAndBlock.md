# callbackblock

        NSMutableDictionary *dinnerRequest = [NSMutableDictionary 
                                              dictionaryWithDictionary:@{
                                                                          @"Don" : @"tofurkey",
                                                                          @"Sandy" : @"burrito",
                                                                          @"Julius" : @ "Chicken
                                                                          }];

        [dinnerRequest enumerateKeysAndObjectsUsingBlok: ^(id key, id value, BOOL *stop) {
                                                          NSLog(@"key: %@, value: %@\n",key,value);
                                                          ];
                                                 //print out all pairs
                                                 
                                                 
# In Swift using ObjectiveC types                                   
        var myDict: NSMutableDictionary = ["Don":"tofurkey","Sandy":"burrito","julius":"Chicken"]
                  
                  myDict.enumerateKeysAndObjects{ (a,b,c) in
                      print(a,b)
                      print(c.pointee)
                  }
                  
                  //print out all pair

#Real way in Swift  

                  var myDict = ["Don":"tofurkey","Sandy":"burrito","julius":"Chicken"]

                  for (_,b) in myDict.enumerated(){
                          print(b.key,b.value)
                  }











#  syntax  ^{...}

# example 1.

      ^{ 
            NSLog(@"print me");
        };
        
 # example 2.
 
      ^(id x, id y){
          NSLog(@"%@, %@,x,y);
        };
        
        compare to swift where you can pass ANY inside
        
        { (x,y) in
          
             print(x,y)
          
        }
        
        
