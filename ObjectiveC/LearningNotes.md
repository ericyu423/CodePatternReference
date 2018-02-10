Reason: Maintaining an App using ObjC

https://www.youtube.com/watch?v=KCnSIZ07QHg

      - (int)match:(Card *)card;
      
in swift
     
      func match(_ card: Card) -> Int {
      }
      
      
now to declare function in objc

# == compare pointer address, isEqualToString look for what is inside the address and compare them

    - (int)match:(Card *)card {
	        int score = 0;
          if( [card.contents isEqualToSTring: self.contents]){
	           score = 1
          }
	        return score;
    }
    
    
what if there is an array of Cards
# * all objects need to use the * notation 

        - (int)match:(NSArray *)otherCards {
	        int score = 0;
          
            //other cards in an array 
            //I guess this is like as! Card in swift
            // * infront of card unlike swift
          
          for(Card *card in otherCards){
            if( [card.contents isEqualToSTring: self.contents]){
	              score = 1
              }
           }
              
              
              
	        return score;
      }
      
# [] vs .

# use . for getter and setters [] for method

note: you can use . notation for methods that takes no argument, but don't do that
