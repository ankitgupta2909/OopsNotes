# POINTERS
int a=10;
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


# 




