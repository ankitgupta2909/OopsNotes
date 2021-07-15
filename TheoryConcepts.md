# Encapsulation

Encapsulation is the process of combining data and functions into a single
unit called class. In Encapsulation, the data is not accessed directly; it is
accessed through the functions present inside the class. In simpler words,
attributes of the class are kept private and public getter and setter methods
are provided to manipulate these attributes. Thus, encapsulation makes the
concept of data hiding possible.  

# Abstraction

We try to obtain an abstract view, model or structure of a real life problem,
and reduce its unnecessary details. With definition of properties of
problems, including the data which are affected and the operations which
are identified, the model abstracted from problems can be a standard
solution to this type of problems. It is an efficient way since there are
nebulous real-life problems that have similar properties

- Advantages are mainly data hiding and error avoidance.  

- Data binding : Data binding is a process of binding the application UI and
business logic. Any change made in the business logic will reflect directly to the
application UI.

# Inheritance

Inheritance is a process in which one object acquires all the properties and
behaviors of its parent object automatically. In such a way, you can reuse,
extend or modify the attributes and behaviors which are defined in other
classes.  
In C++
, the class which inherits the members of another class is called
derived class and the class whose members are inherited is called base class.
The derived class is the specialized class for the base class.  

- **Access Modifiers**
  Private: Only functions of same class  
  Public: Anyone  
  Protected: Only child classes can access, Not even by itself similat to private   

Syntax:  

class Vehicle{  
    private:  
        int maxSpeed;  

    protected:  
        int numTyres;  
    
    public:  
        string colour;
};

- class Car : public Vehicle{  
    // private wont be inherited  
    // public will be public here  
    // protected will be protected  
    }  

You can use and access properties just like they belong to  the child class only , no extra keyword.   

- class Car : protected Vehicle{  
    // private wont be inherited  
    // public will be protected here  
    // protected will be protected  
    }  

- class Car : private Vehicle{  
    // private wont be inherited  
    // public will be private here  
    // protected will be private    
    }  

    if we dont mention access modifier, It is private by default  

**Constructors in inheritance**

- By default, parent class constructors get called when we create a variable of any child class.  
- If u make a constructor in any class, make sure u make a default constr too cz it will be called while object creation of child class.  
- How to make a parametrized constructor in child class?  
  Car(int x): Vehicle(x){  
      // that : Vehicle() is done by default if not mentioned for unparameterized constr.  
  }  
  and in vehicle class  
  Vehicle(int x){
      this.x=x;  
  }  

  A class can only call constr of its immediate parent not granndparent.  
- Destrtuctors are called in reverse manner of constr. like child first then parent.  
  
*Types of Inheritance*
- Single Inher.  
- Multi level Inher.  
- Hirarchial Inher. : One inherited by many  
- Multiple Inher: Multiple parents  
  Syntax:  
  class Teacher{    
      public:  
      string name;  
      string age;  
      void print(){  
          print(teacher);
      }
  };  
class Student{
    public:  
     void print(){  
          print(Student);  
      }  
};  
class TA: public Teacher,public Student{  
    // constr of teacher will be called first cz written first,then Student  
};    

TA x;
x.print();  // Error cz of ambiguity  
x.Student:: print();  //Right way 


if we have a print() in our class then only it will look above else just access our own object.  

- Hybrid Inher. : Combination of all example: Diamond shape  

- Order of calling constr.  
  vehicle  
  car->vehicle  bus->vehicle   
  truck->car,bus  

  1-vehicle()  
  2-car()  
  3-vehicle()  
  4-bus()  
  5-truck()  

  **Virtual Base Class**
- If we want just 1 copy of vehicle in above example ,we can use virtual class  

  vehicle  
  car->virtual vehicle  bus->virtual vehicle   
  truck->car,bus  

  1-vehicle()  
  2-car()   
  3-bus()  
  4-truck()    
// Vehicle() only called once   

- What virtual class means is we just give a pointer to class and not the actual class while inher.  
-  If we make virtual inheritance , child class calls the constr of grand parent too unlike just of immediate parent before.Infact, in diamond inher prob, car, bus dont even call for the constr first, the  truck obj calls the constr. we can check using parametrised constr..  


# Polymorphism

- Polymorphism is the ability to present the same interface for differing
underlying forms (data types). With polymorphism, each of these classes
will have different underlying data.  

- Types of Polymorphism  
1. Compile Time Polymorphism (Static)  
2. Runtime Polymorphism (Dynamic)  

● **Compile Time Polymorphism** : The polymorphism which is implemented at
the compile time is known as compile-time polymorphism. Example -
Method Overloading  

 **Method Overloading** : Method overloading is a technique which allows you
to have more than one function with the same function name but with
different functionality. Method overloading can be possible on the
following basis:  
1. The return type of the overloaded function.  
2. The type of the parameters passed to the function.  
3. The number of parameters passed to the function.

- Also, when we made function print in truck,it stopped looking above , it is function overriding.

- Base class pointer can point to derived class obj but not vice vis.  
    And also we can only access props or function using pointer which are also present in base/parent class.  
- At compile time, we compiler doesnt see the pointer is holding ref of which class, it just sees the class of which the pointer is and calls its method.  

Example:  
#include <bits/stdc++.h>  
using namespace std;  
class Base_class{  
public:  
virtual void show(){  
cout << "Apni Kaksha base" << endl;  
}  
};  
class Derived_class : public Base_class  {  
public:  
void show(){  
cout << "Apni Kaksha derived" << endl;  
}  
};  
int main(){   
Base_class* b;   
Derived_class d;    
b = &d;  
b->show(); // prints the content of show() declared in base class   


- **Runtime Polymorphism** : 
  Runtime polymorphism is also known as dynamic
polymorphism. Function overriding is an example of runtime
polymorphism. Function overriding means when the child class contains
the method which is already present in the parent class. Hence, the child
class overrides the method of the parent class. In case of function
overriding, parent and child classes both contain the same function with a
different definition. The call to the function is determined at runtime is
known as runtime polymorphism.

Example:  
#include <bits/stdc++.h>  
using namespace std;  
class Base_class{  
public:  
virtual void show(){  //here  
cout << "Apni Kaksha base" << endl;  
}  
};  
class Derived_class : public Base_class  {  
public:  
void show(){  
cout << "Apni Kaksha derived" << endl;  
}  
};  
int main(){   
Base_class* b;   
Derived_class d;    
b = &d;  
b->show(); // prints the content of show() declared in derived class   

- Look closely, virtual function is used to enforce run time polymorphism.  
- If there is no show() in derived class, we call the parent class show(), but if parent class doesnt have a show() it will show error.   

**Abstract Classes**

*Pure virtual functions*
    virtual void print()=0; 
It is just an incomplete function   
Any class having pure virtual function is called Abstract class.  
It helps in run time polymorphism.  
Any class that inherits abstract class has two options:  
Either complete all the pure virtual functions and become normal class.  
Or become abstract as well.  
Also, u cant create an obj of an Abstract class, it throws an error.  
It is used when we want run time polymorphism for a function but it cant be defined in the parent class, so we declare it in parent virtually to achieve  run time polymorphism and define later in derived class.  

**Friend Class**

Friend Class A friend class can access private and protected members of other class in which it is declared as friend. It is sometimes useful to allow a particular class to access private members of other class. For example, a LinkedList class may be allowed to access private members of Node.   

Example:  
class Node {  
private:  
    int key;  
    Node* next;  
    /* Other members of Node Class */  
 
    // Now class  LinkedList can  
    // access private members of Node  
    friend class LinkedList;   
};  

*Friend Function*  
Friend Function Like friend class, a friend function can be given a special grant to access private and protected members. A friend function can be:   
a) A member of another class   
b) A global function   

Example:   
class Node {    
private:  
    int key;  
    Node* next;  
    /* Other members of Node Class */  
 
    // Now class  LinkedList can  
    // access private members of Node  
    friend int LinkedList::search();
};  
Following are some important points about friend functions and classes:   
1) Friends should be used only for limited purpose. too many functions or external classes are declared as friends of a class with protected or private data, it lessens the value of encapsulation of separate classes in object-oriented programming.  
2) Friendship is not mutual. If class A is a friend of B, then B doesn’t become a friend of A automatically.  
3) Friendship is not inherited  
4) The concept of friends is not there in Java.   
5) Access using :: like => A::x=v;  

Read about exception handling  