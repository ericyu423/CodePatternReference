heapMemory(review)


local variables are allocated in the stack frame, using stack memory
stack memory is recyele when a frame is destroyed (done using)
so if you to a recursive call, keep calling a function you get a stack overflow

so if you point to a local variable and the local variable is destoryed you might get something weird back.
(I remember learning this in C...)
the address can get recycled so the old address might have something else in it.

leak memory (same as swift for example strong reference cycle)
once allocated memory init so you don't get garbage

sizeof(<type>) example sizeof(int) you get enough memory to store int (I remember this when working with openGL)

int = x;
a = &x; // you get an address in the stack

a = malloc(sizeof(int));// you get an address in the heap
.
.
.
free(a); //free it once you don't use it anymore

malloc return an adress of size int 


objectiveC

isntead of
MyTime *a = malloc(sizeof(MyTime))// allocated enough memory in heap for type MyTime
use

MyTime *a = [MyTime alloc];
