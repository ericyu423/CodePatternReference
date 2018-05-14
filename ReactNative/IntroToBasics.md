# folders


  node_modules -  contain dependencies it folder contain a dependency 
  root files -  .[name] for for configurations 
  index.js - entry point of our app
  
  
  # React  vs React Native
  
       React -> know how a component should behave, what function it should have and to a lot of components and make them work togehter
      
       React Native -> output to mobile device
       
       
  example program:
  
      import React from 'react';
      import { Text, AppRegistry } from 'react-native';

      const App = () => <Text>Some Text</Text>;

      AppRegistry.registerComponent('albums', () => App);
   
 # $ react-native run-ios
      
 run on terminal the first time you might get an error
 
 fix error
 xcode->preference->Location->commandline Tool -> select a version of xcode (Xcode 9.3.1(9E501)) for me 5/14/2018

# $ react-native run-android
    need to have simulator open first or else it will not work
    
 # folder structure
 
        src ---components ---header.js
                          ---      .js
                          ---      .js
 
