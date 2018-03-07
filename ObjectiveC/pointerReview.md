Is pretty much like C

          void addFive(int *somePointer){
              (*somePointer) = (*pointerPointer) + 5;

              //stuff in address of somepointer add five to it

          }


          int main(){
            int x = 2;
            int *pointerToX = &x;
            addFive(pointerToX);

            //x is now 7
            //so pretty much you can think of it as, rather than adding variable on a stack
            //we stole the address of x, go in the heap find where x lives
            // and add stuff directly to it


            return 0
          }


          int y = 5;
          int *x = &y;
          (*x) = 6;

          y = 6;
