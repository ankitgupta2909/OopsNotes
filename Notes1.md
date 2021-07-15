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

  
- int a=10;  
  int * pa=&a;  
  pa++;     //pointer jumps 4 bytes cz its int pointer 1 for char,8 for double  it looks for next int/char/double
  
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

  int ar[]={1,2,3};  
  char cr[]="abc";  
  it is same as => char str[4] = {'a','b','c','/0'};  
  cout<<ar; // Adrress of  a  
  cout<<cr; // String abc prints  


- char a='x';  
  cout<<a;      // prints x  
  char *pc=&a;  
  cout<<pc;     // Traverse til finds \0 nd prints example: x?/;  

- U cant do *ptr="abc";  this is allocation of a temporary memory to pinter 

---

**Functions pointer**

- 
  void fun1(int *p){
      cout<<*p;         //Noramlly prints  
    }  
  void fun2(int *p){  
      p=p+1;            //Doesnt change the address of p its passed by value   
  }  
  void fun3(int *p){  
      (*p)++;               // Actually changes the value stored at address p  
  }  

- if i send something like 
    int *a={1,2,3,4,5,6,7,8,9};  
    fun(a+4);    //This just send array from 4th index and onwards to the function  
    
- *Double Pointer*
  int a=10;
  int *a1=&a;
  int **a2=&a1; // Pointer to pointer  holds address of pointer which holds address of a

---


# Dynamic Allocation

- Reason why we put int *x not just pointer x when we know every pointer just takes 4/8 bytes is to get to know how many bytes to jump or traverse in one increment like +4 for int +1 for char etc.
  
- 
  int i=65;    
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

   What we conclude here is integers are stored reversed

**Reference Variable**

-int a=10;  
int &b=a; // Has ref of a anychange made will be reflected on both dont hold any memory point to same  
It has to be intitialised in the same line.  

- If we return ref var or a pointer from a funtion like this
   
   int* fun(int a){  
       return a;  
   }  
  
   int &f=fun(a);  

   OR 

   int* fun(int a){
       return &a;
   }

   int *ptr=fun(a);
   

   There is a prob that memory has a scope til that function only and will be destroyed so u may get error for accessing garbage

-

** Stack space and Heap space**

-we should never do something like  
    int n;  
    cin>>n;  
    int ar[n];  
This may cause error because there is limmited stack space and n may be large

- Stack space is allocated on compile time that means int a,int c=10,int arr[a],int arr[100000], all these will be allocated in stack and some empty space will be kept for rest of function.Also called static.  

- Dynamic Allocation is done using new  
    int *a=new int;  
  Now we can solve our old issue,  
  int n;  
  cin>>n;  
  int *ar=new int[n];  

- Dynamically allocated memory never destroys itself
  ex:  
  while(1){
      int x=10;
  }
  only const space filled  
    but  
  while(1){  
      int *x=new int;  
  }  
  space overflow  


- We use delete(var); to deallocate the dynamically allocated memory
   For array delete []var;

-* Dynamic Allocation of 2d array*
  
  int n,m;  
  cin>>n>>m;  
  int **p=new int\*[n];  
  for(int i=0;i<n;i++){  
      int *row=new int[m];  
      for(int j=0;i<m;j++){  
          cin>>p[i][j];  
      }  
  }  
  for(int i=0;i<n;i++){  
      delete []p[i];  
  }  
  delete []p;  


- Define is used for declaring a few pre processor dircetives,ex  
  define a 10

  now compiler will read every a as 10

- Inline is used to simplify the function process ,compiler just copies the code while executing in the code  
  Dont use it much cz compiler ignore if its too big  

**Const Keyword**

- Cant change its value obviously

- const int a=10;  
  int &b=a; //Throws error cant create a non const ref of a const var

- int a=10;
  const int &b=a;  // No error till here
  b++;   // Throws error u cant change a const var

-By ref u create a channel to the var,if the channel is const u cant update ,if var is const u can only create a const channel

- Same for pointer, u cant create a normal pointer to a const var
  const int x=0;
  int *xp=&x;    // Error it is not possible
  int const *xp=&x; // This is right

- Critical point
  const int i=10;  
  const int j=20;  
  int const *p=&i;  //p is pointer to a const int  
  p=&j;  //U can assign p to another const var no issue 
  *p++;  //Error 
  int * const p2=&i;  //p2 is a const pointer to an integer   
  (*p2)++;  //No issue
  p2=&j;   // Error u cant change whats const  

  int const * const p3 =&i; //p3 is a const pointer to a const var   
  p3=&j;  //error  
  (*p3)++;  //error  
