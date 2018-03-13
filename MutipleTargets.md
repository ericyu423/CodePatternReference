# Objective C


blue project icon -> [one of your target] -> build settings
                      --> preporcessor Marcos
                         
                         
                                  
                             example (for 3dazer, pro version )
                                                DEBUG=1 COCOAPODS = 1 PRO = 0 HOME = 0
                                                        COCOAPODS = 1 PRO = 0 HOME = 0
                                  
                             example ( for 3daer pro, version only for internal testing)
                                                DEBUG = 1 COCOAPODS = 1  PRO = 1 HOME = 0
                                                           COCOAPOD = 1  PRO = 1 HOME = 0
                                              
                                              example, (for home dazer Home target, version will less functionality)
                              debug           DEBUG = 1 COCOAPODS = 1  PRO = 1 HOME = 0
                                              RELEASE     COCOAPODS = 1,PRO = 1  HOME = 0
                                             
                                             
basically there are 2 version different in preprocessor

use this in app by

                                  #if PRO
                                  #define ISPROAPP YES
                                  #else
                                  #define ISPROAPP NO
                                  #endif

                                  #if HOME
                                  #define ISHOMEAPP YES
                                  #else
                                  #define ISHOMEAPP NO
                                  #endif



# FOR SWIFT
   
   
       build settings
       
        swift compiler - custom Flags -> other swift falgs -> -DDEVELOPMENT
        
        
       
                                              #if DEVELOPMENT
                                          
                                              #else
                                           
                                           
                                              #endif
   
