# POINTERS
-int a=10;
int *ap=&a;
- &: address
- *: Dereferencing (value)
- Symbol table: Map of address and variables
- int: 4 bytes
- pointer to int/char/double all: 8 bytes(not fixed)
  
-  (*p)++;  // Increments the value of var held by address stored in p

- int *p=0; // Always reference the pointer or it will point to a random address holding garbage and may not even be in our scope..it can cause error.. referencing to 0 means null.will always cause erro but betterthan random

  
- `int a=10;  
  int * pa=&a;  
  pa++;     //pointer jumps 4 bytes cz its int pointer 1 for char,8 for double  it looks for next int/char/double
`  
- a[i]=i[a]= *(a+i) // int a[10]; in this a is nothing but pointer to first el

- int a[10];  
  sizeof(a)=40;  
  whereas in pointer.. sizeof(*p) is always 4 or 8 dep on system  

- when we print a it gives address, when we print &a it again gives same address
  it means a doesnt have a memory allocated to itself like pointers where printiing p and &p used to diff addresses

- a= a+2 / a++ / a-- is illegal
---
**Char array**

- Printing works diff if int and char array
`
  int ar[]={1,2,3};  
  char cr[]="abc";  
  cout<<ar; // Adrress of  a  
  cout<<cr; // String abc prints  
`
`
- char a='x';  
  cout<<a;      // prints x  
  char *pc=&a;  
  cout<<pc;     // Traverse til finds \0 nd prints example: x?/;  
`
- U cant do *ptr="abc";  this is allocation of a temporary memory to pinter 

---

**Functions pointer**

- `
  void fun1(int *p){
      cout<<*p;         //Noramlly prints
    }
  void fun2(int *p){
      p=p+1;            //Doesnt change the address of p its passed by value 
  }
  void fun3(int *p){
      (*p)++;               // Actually changes the value stored at address p
  }

- *Double Pointer*
  int a=10;
  int *a1=&a;
  int **a2=&a1; // Pointer to pointer  holds address of pointer which holds address of a

---


# Dynamic Allocation

- Reason why we put int *x not just pointer x when we know every pointer just takes 4/8 bytes is to get to know how many bytes to jump or traverse in one increment like +4 for int +1 for char etc.
  
- 
  `int i=65;    
   char c=i;         Implicit typecasting prints A cz ascii  
   int *p=&i;  
   char *pc=&p;   throws error     
   char *pc=(char star) &p;  Explicit typecasting    
   cout<<p;   Prints address of i 
   cout<<pc;  Prints till finds \0 so just A will be printed   
   cout<<*p;  65  
   cout<<*pc;  Prints what is there at LSB of p   |65|-|-|-| (4 bytes of integer and we are doing only 1 byte inc in char pointer)   
   cout<<*pc+1;  right of lsb   
   cout<<*pc+2; next right of lsb  
`
   What we conclude here is integers are stored reversed

**Reference Variable**

-int a=10;
int &b=a; // Has ref of a anychange made will be reflected on both
It has to be intitialised in the same line.

- If we return ref var or a pointer from a funtion like this
   
   `int* fun(int a){  
       return a;  
   }  
  
   int &f=fun(a);  

   OR 

   int* fun(int a){
       return &a;
   }

   int *ptr=fun(a);
   `

   There is a prob that memory has a scope til that function only and will be destroyed so u may get error for accessing garbage





