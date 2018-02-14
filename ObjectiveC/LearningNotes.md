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


# make optional arugments for functions

	create mutiple functions with same name with 1, 2 , 3... arguments. They are actually distinct
	
# Property in .m file
	put in .h file is same as 
	public in swift
	while put in .m file is same as
	private in swift
# atomic vs non-atomic (use nonatomic)
	atomic let you deal with multiple threads with locking
	non-atomic you can use it in one thread
# Strong vs Weak reference (same as swift)
	strong reference meanings holding on to the object, as long as you or anyone else hold on to it, it won't get destroy
	weak reference means touching the object sort of, you can do everythign the same as strong, however,
	if someone else let go, it will get destroyed.
	
# side note (swift owned -  sort of like weak) NON OPTIONAL 
	owned always have a value (not optional)


	two classes where one can not exist without another.
	vistor hold strong reference to annual pass
	person hold strong rerference to credit card
	
	credit card, annual pass are two thing created by the vistor or person
	so both annual pass or credit card are owned pointer back to visitor.
	
	A unowned reference must be set during initialization
	
# function -  class function + (class method)

