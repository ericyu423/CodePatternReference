


      UILabel *label = [[UILabel alloc] init];
      
      UILabel *label = [UILabel new];
      
      
      
      
      
      
      struct Time {
        int a;
        int b;
        int c;
      };
      struct Time mytime;
      
      mytime.a = 3
      
      typedef struct {
          int a;
          int b;
          int c;
       } Time;
       
       Time mytime;
       
       mytime.a = 3


            @interface MyTime: NSOBject
            
            @property int hour;



           MyTime *time = [MyTime alloc];
           time.hour = 10;  <---->   [time setHour: 10];  //there are the same
           
           
           int a,b;
           
           a = time.hour; <----> a = [time hour];  //these are the same
