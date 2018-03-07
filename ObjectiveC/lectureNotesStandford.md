
# Lecture2 notes


# instancetype (always this pattern)

call by PlayingCardDec myCard = [[PlayingCardDec alloc]init]// only do this once u can't init twice

          @implentation PlayingCardDec
          - (instancetype)init
          {
              self = [super init]; //so super class get initialized and assign to self
                                    //reason if initializer can not initiallzied it self
                                    //it should return nil

              if (self) {



              }

              return self; //return instance type


          }
          @end








# ------------




      -(Card *)drawRandomCard
      {
          Card *randomCard = nil;
          
          if([self.cards count]){// add this if array have elemnent
          //or array can crash the program out of bound error
            unsigned index = arc4random() % [self.cards count];
            randomCard = self.card[index];
            [self.cards removeObjectAtIndex:index];
          }
          
          return randomCard;
       }
       



# PlayingCard.h

        @interface PlayingCard: Card 
        @property (strong, nonatomic) NSString *suit; 
        @property (strong, nonatomic) NSUInterger rank;
        
          + (NSArray *)validSuits; // add this to make it public
       
# PlayingCard.m

          #import "PlayingCard.h"
          //why interface is not declared here ?  @interface PlayingCard() ..... @end

          @implementation PlayingCard
          -(NSString *)contents
          {
            NSArray *rankStrings = @[@"?",@"A",@"2"];
            return [rankString[self.rank] stringByAppendingString:self.suit]
          }//basically get one of the ranking symbols from rank(index) and append to self.suit string
           //return the result...such as [Club]2

           @synthesize suit = _suit; // because we provide setter and getter

          -(void setSuit:(NSString *)suit
          {
              if[@[@"C",@"D",@"H",@"S"] containsObject:suit]){
                  _suit = suit;
               }
               
               //or rewite as make it look better, performance diff is negligible 
                if([[PlayingCard validSuits] containsObject:suit]){
                  _suit = suit;
               }
          }
          
          + (NSArray *)validSuits {
              return @[@"C",@"D",@"H",@"S"]
          }
          
          -(NSString *)suit
          {//getter if suit contain one of C,D,H,S return it otherwise return "?"
              return _suit ? _suit : @"?";
          }
          
          @end
