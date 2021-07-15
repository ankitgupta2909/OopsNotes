**Object-Oriented Programming is a methodology or paradigm to design a
program using classes and objects. It simplifies the software development
and maintenance by providing some concepts defined below :**

# Class
- Class is a user-defined data type which defines its properties and its
functions. Class is the only logical representation of the data
- class Student{  
 int rollno;  
 string name;  
 int grades[6];  
 int age;  
 };   

- Static allocation
   Student s1;

- Dynamic Allocation
  Student *s2=new Student;  

- #include"Student.cpp"  //includes the class if code is present in that file

- To access or change in statically allocated object s1.age=30;  . is used to initialise/access statically allocated objects  
- Same for dynamic is (*s1).age=30;  or we can write s1->age=30;  -> is used to initialise/access dynamically  allocated objects


 **Access Modifiers**
  private = only confined to class  
  public = even outside  
  protected =   
  by default = private  

**Constructors**
- Same name as class, no return type.
- Default constr. =>  
  Student(){  
  
  }  
- Student(int r){  
  rollno=r;  //parameterized constr.
  }  

- When we make our own constr. default constr wont work, so u cant just define vars like Student s1;
  It will show error cz no default constr is there,u have to write it.  

-*this*
    It holds the address/instance of cur object. example:  
    Student(int rollno){  
        this.rollno=rollno;  
    }  
*this* just has a address it is a pointer,works exactly like pointer. 


**Copy Constructor**

- We can do Student s2(s1);  to copy all props of s1 in s2 i.e s2.age=s1.age etc  
  For dynamically:  
    Student s4=(*s3);  

This was default copy constructor  
- s2=s1 copies all props of s1 to s2.. It is copy assignment operator. 
- Student s5=s4;  Copy constructor will be called not assignment operator. 

**Destructor**

- ~Student(){  
  }  

- Executes just before end,deallocates memory allocated to class object
- For dynamically allocated obj destructor wont be clled we have to do delete explicitly. 

**Deep/ Shallow copy**

- When we copy such that the change in 1 gets reflected in other,its shallow.Which means address is copied and new var isnt created. This happens when we default copy arrays like:  
  char name[]="abcd";  
  Student s1(20,name);  
  s1.display();  //abcd  
  name[3]='e';  // We changed the  array  
  Student s2(24,name);  //Shallow copy happening in class    
  s2.display();  //abce  
  s1.display();   //abce  (Change in the original gets reflected)  

- Example:  
  Student{  
    int age;  
    char* name;  
    public:  
    Student(int age,char* name){  
      this.age=age;  
      this.name=name;   //Shallow copy  
      this->name= new char[strlen(name)+1];  
      strcpy(this->name,name);      // Deep copy  
    }  
    Student(Student s){   
      this.age=s.age;  
      this.name=s.name;   //Shallow copy (this happens when we do Student s2(s1))  
      this->name= new char[strlen(s.name)+1];  
      strcpy(this->name,s.name);      // Deep copy  
    }  
  }  
- *important point*
Student(Student s){   // Here a default copy constr is called to create an object s but as we are making our own constr ,default copy constr is ruled out,this will form loop and end up in error   
      this.age=s.age;  
      this->name= new char[strlen(s.name)+1];  
      strcpy(this->name,s.name); 
    }  

    So, to solve this thing..  
We do this:=>  
Student(Student &s)  // So that reference is passed and copy is not needed hence no copy constr  
Also ,make it const like Student (Student const &s)  
So that we cant make changes in s  


**Initialisation List**

- We have to initialise constant and reference var at the time of creation or they will be given garbage and throw error. But, in classes if we want an object to be const it cant be given value there only cz then it will be same for all objects. This is issue is solved using Initialistaion List.  
- Syntax:    
  class Student{    
    public:    
    int age;    
    const int rollno;   
    int &x;   
    Student(int r,int age): rollno(r),age(age),x(this->age)  {    
    }   
  }   

**Constant Variable of classes**

- U can only access const functions of class using a const var. 
- Example:  
  class Student{  
    int age;    
    int rollno;    
    public:     
    void setAge (int age) const {
      this.age=age;  
    }  
    void getAge(){  
      cout<< age;  
    } 
    void getAgeNew() const  {  
      cout<< age;  
    }    
  }  
  
  int main(){  
    Student const s / const Student s1;  
    s1.getAge();  // Shows error coz function not const  
    s1.getAgeNew(); //No error  
    s1.setAge(10);  // No error here but error in class cz cant change using const function  
  }   

- Onlymark those function const which dont change anything


**Static Members**

- If a property is shared by all objects but belongs to no one but the class .. its static. 
- They  work like global but confined to objects of the class.
- class Student{  
 int rollno;  
 static int strength;
 };    
int Student :: strength=0;  // This is how we initialise static member..Its done outside the class  

- We can access and update static members like normal vars example:  
  class Student{  
 int rollno;  
 static int strength;
 Student(){  
   strength++;  
 }  
 };   
 int Student :: strength=0; 

 int main(){  
   Student s1;  
   s1.strength=20;  
   cout<< s2.strength;  // This will print 20  
 }   
 But this is not ideal  

 What we should do ideally is:  
 Access using:  Student :: strength;
 Update?Access using:  
  static void update(int n){  
   strength+=n;  
 }  

 Remember that static func can only access static members,they dont have 'this' keyword and are called without using any var simply Student::update(8);


 **Operator Overloading**
- We can define operators like + - == / for objects of our class like:  
  Student operator+(Student s){  //operator is a keyword and followed by the operator(+/-==)  
    return this.marks+ s.marks;  
  }  
  In such functions we accept only one var cz it automatically takes first var as 'this' var.  
  Call=>  
  Student s3=s1+s2;  // its similar to s1.add(s3) if we implemented add function   
  Here s1 is this and s2 is var passed  

*Unary Operator overloading*

- Lets implement ++(pre) operator:  
  void operator++(){  
    this.a=this.a+1;   // this key is optional  
  }  
This simply increments   
  int operator++(){  
    this.a=this.a+1;  
    return *this;  // Returning our value to save when called like student x=++a;  
  }  
But what if we do something like x=++(++a)  
This will increment a only once cz next time,we create temporary copy of a and increment it and save in x but wont change a  
So to avoid such mistakes  
int& operator++(){  //We use reference in return type so we dont create copy but change the instance itself  
  this.a=this.a+1;  
  return *this;  
}   

- To implement post increment:  
  int operator++(int){ 
    int x=this.a; 
    this.a=this.a+1;  
    return x;    
  }  
And (a++)++ isnt allowed nesting  

*Try to implement dynamic sized array class using concepts discussed above*   


