
Clean Code
===================

Robert C. Martin

----------

  

Test-driven development (TDD)
-------------
![](http://www.agiledata.org/images/tddSteps.jpg)


Open Closed Design Principle
-------------
Classes, methods or functions should be Open for extension (new functionality) and Closed for modification. This is another beautiful SOLID design principle, which prevents someone from changing already tried and tested code.

Let’s see a simple example to better understand it. We will need a strategy interface, a class that uses the strategies, the context class, and some implementation of the strategy interface.

    public interface Strategy {
    
     public void doSomething();
    
    }
    
      
    
And a context class that encapsulates a strategy implementation and executes it.
    
    public class Context() {
    
     private Strategy strategy;
    
     // we set the strategy in the constructor
    
     public Context(Strategy strategy) {
    
     this.strategy = strategy;
    
     }
    
     public void executeTheStrategy() {
    
     this.strategy.doSomething();
    
     }
    
    }
    
      
    
And let’s create two implementations for the Strategy interface.
    
    public class Strategy1 implements Strategy {
    
     public void doSomething() {
    
     System.out.println(“Execute strategy 1”);
    
     } 
    
    }
    
    public class Strategy2 implements Strategy {
    
     public void doSomething() {
    
     System.out.println(“Execute strategy 2”);
    
     } 
    
    }

Now we can bind this together. The idea is to send to the context class the strategy we want to run. Like I said before, you can use Dependency Injection or the factory pattern for this, but it’s out of this article’s scope, so let’s just make a simple Demo class to see how it works.

    public class Demo() {
    
     public static void main(String[] args) {
    
     Context context = new Context(new Strategy1()); // we inject the Strategy1
    
     context.executeTheStrategy();  // it will print “Execute strategy 1”;
    
     context = new Context(new Strategy2());  // we inject the Strategy2
    
     context.executeTheStrategy();  // it will print “Execute strategy 2”
    
     }
    
    }

So the context is decoupled from a specific strategy class. You could implement however many strategies you want and no matter how they work and what you want them to do, you don’t need to modify the context class. The context class knows just that it must call doSomething method and it is enough.


Single Responsibility Principle (SRP)
-------------
Single Responsibility Principle is another SOLID design principle, and represent "S" on the SOLID acronym. As per SRP, there should not be more than one reason for a class to change, or a class should always handle single functionality.  
  
If you put more than one functionality in one Class in Java it introduces **coupling** between two functionality and even if you change one functionality there is a chance you broke coupled functionality, which requires another round of testing to avoid any surprise on the production environment.  

Take a look at the  `Employee`  class below –  

    Employee.java
    public class Employee{
      private String employeeId;
      private String name;
      private string address; 
      private Date dateOfJoining;
      public boolean isPromotionDueThisYear(){
        //promotion logic implementation
      }
      public Double calcIncomeTaxForCurrentYear(){
        //income tax logic implementation
      }
      //Getters & Setters for all the private attributes
    }

The above  `Employee`  class looks logically correct. It has all the employee attributes like  `employeeId`,  `name`,  `age`,  `address`  &  `dateOfJoining`. It even tells you if the employee is eligible for promotion this year and calculates the income tax he has to pay for the year.

However,  `Employee`  class breaks the Single Responsibility Principle. Lets see how  –

-   **The logic of determining whether the employee is due this year is actually not a responsibility which the employee owns.**  The company’s HR department owns this responsibility based on the company’s HR policies which may change every few years. On any such change in HR policies, the Employee class will need to be updated as it is currently has the responsibility of promotion determination.
-   **Similarly, income tax calculation is not a responsibility of the Employee.**  It is the finance department’s responsibility which it takes care of the current tax structure which may get updated every year. If Employee class owns the income tax calculation responsibility then whenever tax structure/calculations change Employee class will need to be changed.
-   **Lastly,  `Employee`  class should have the  _single responsibility_  of maintaining core attributes of an employee.**

Refactoring the Employee class so that it adheres to Single Responsibility Principle  
Let us now refactor the  `Employee`  class to make it own a single responsibility.

Lets move the promotion determination logic from  `Employee`  class to the  `HRPromotions`  class like this –  


    HRPromotions.java
    public class HRPromotions{
      public boolean isPromotionDueThisYear(Employee emp){
        //promotion logic implementation using the employee information passed
      }
    }


Similarly, lets move the income tax calculation logic from  `Employee`  class to  `FinITCalculations`  class –  


    FinITCalculations.java
    public class FinITCalculations{
      public Double calcIncomeTaxForCurrentYear(Employee emp){
        //income tax logic implementation using the employee information passed
      }
    }

Our  `Employee`  class now remains with a single responsibility of maintaining core employee attributes –  

    Employee.java adhering to Single Responsibility Principle
    public class Employee{ 
      private String employeeId;
      private String name;
      private string address; 
      private Date dateOfJoining;
      //Getters & Setters for all the private attributes
    }


 Dependency Injection or Inversion principle
-------------
It represents "D" on the SOLID acronym

    public class AuditServiceImpl implements AuditService{

    private AuditDAO auditDao;

    public void setAuditDao(AuditDAO AuditDao) {
        this.AuditDao = AuditDao;
    }
  
    @Override
    public boolean audit (String message) {
       return auditDao.store(message);
    }
  
	}


Favor Composition over Inheritance
-------------

Always favor composition over inheritance, if possible. Some of you may argue this, but I found that Composition is the lot more flexible than Inheritance

Composition allows **changing behavior of a class at run-time by setting property** during run-time and by **using Interfaces to compose a class we use polymorphism** which provides flexibility of to replace with better implementation any time.  

For example, take a set of classes DynamicDataSet and SnapShotDataSet that require a common  
functionality—say, sorting. Now, one could derive these data set classes from a sorting implementation, as

    //Sorting.java
    
    import java.awt.List;
    
    public class Sorting {
    
     public List sort(List list) {
    
     // sort implementation
    
     return list;
    
     }
    
    }
    
    class DynamicDataSet extends Sorting {
    
    // DynamicDataSet implementation
    
    }
    
    class SnapshotDataSet extends Sorting {
    
    // SnapshotDataSet implementation
    
    }

In this case it is best to use composition

    //Sorting.java
    
    import java.awt.List;
    
    interface Sorting {
    
     List sort(List list);
    
    }
    
    class MergeSort implements Sorting {
    
     public List sort(List list) {
    
     // sort implementation
    
     return list;
    
     }
    
    }
    
    class QuickSort implements Sorting {
    
     public List sort(List list) {
    
     // sort implementation
    
     return list;
    
     }
    
    }
    
    class DynamicDataSet {
    
     Sorting sorting;
    
     public DynamicDataSet() {
    
     sorting = new MergeSort();
    
     }
    
     // DynamicDataSet implementation
    
    }
    
    class SnapshotDataSet {
    
     Sorting sorting;
    
     public SnapshotDataSet() {
    
     sorting = new QuickSort();
    
     }
    
     // SnapshotDataSet implementation
    
    }

  
Liskov Substitution Principle (LSP)
-------------

https://dzone.com/articles/the-liskov-substitution-principle-with-examples

According to Liskov Substitution Principle, Subtypes must be substitutable for supertype i.e. methods or functions which uses superclass type must be able to work with the object of subclass without any issue".  
  
LSP is closely related **to Single responsibility principle** and **Interface Segregation Principle**. If a class has more functionality than subclass might not support some of the functionality and does violate LSP.  
  
In order to follow **LSP SOLID design principle**, derived class or subclass must **enhance functionality, but not reduce them.** LSP represents "L" on the SOLID acronym.

### Java Code Samples to Illustrate the LSP

    public class Rectangle {
    
     private int length;
    
     private int breadth;
    
     public int getLength() {
    
     return length;
    
     }
    
     public void setLength(int length) {
    
     this.length = length;
    
     }
    
     public int getBreadth() {
    
     return breadth;
    
     }
    
     public void setBreadth(int breadth) {
    
     this.breadth = breadth;
    
     }
    
     public int getArea() {
    
     return this.length * this.breadth;
    
     }
    
    }
    
Below is the code for Square. Note that Square extends Rectangle.

    public class Square extends Rectangle {
    
     @Override
    
     public void setBreadth(int breadth) {
    
     super.setBreadth(breadth);
    
     super.setLength(breadth);
    
     }
    
     @Override
    
     public void setLength(int length) {
    
     super.setLength(length);
    
     super.setBreadth(length);
    
     }
    
    }

The code below represents the function which has Rectangle as an argument. As per the principle, the functions that use references to the base classes must be able to use objects of derived class without knowing it. Thus, in the example shown below, the function calculateArea, which uses the reference of “Rectangle,” should be able to use the objects of derived class, such as Square, and fulfill the requirement posed by Rectangle definition.

Look at the calculateArea method in the code below. One should note that, as per the definition of Rectangle, the following must always hold true given the data below:

-   Length must always be equal to the length passed as the input to method, setLength.
-   Breadth must always be equal to the breadth passed as input to method, setBreadth.
-   Area must always be equal to the product of length and breadth.

In this case, we try to establish an ISA relationship between Square and Rectangle such that calling “Square is a Rectangle” in the below code would start behaving unexpectedly if an instance of Square is passed. An assertion error will be thrown in the case of checking for "Area" and checking for "Breadth," although the program will terminate as the assertion error is thrown due to the failure of the Area check.

	public class LSPDemo {  
  
        /**  
     * One should note that as per the definition of Rectangle, following must always hold true given the data below: * <p>  
     * 1. Length must always be equal to the length passed as the input to method, setLength * <p>  
     * 2. Breadth must always be equal to the breadth passed as input to method, setBreadth * <p>  
     * 3. Area must always be equal to product of length and breadth * <p>  
     * <p>  
     * <p>  
     * In case, we try to establish ISA relationship between Square and Rectangle such that we call "Square is a Rectangle", * <p>  
     * below code would start behaving unexpectedly if an instance of Square is passed * <p>  
     * Assertion error will be thrown in case of check for area and check for breadth, although the program will terminate as * <p>  
     * the assertion error is thrown due to failure of Area check. * * @param r Instance of Rectangle  
     */  
      public void calculateArea(Rectangle r) {  
      
            r.setBreadth(2);  
      
            r.setLength(3);  
      
            // Assert Area  
      
     // From the code, the expected behavior is that   
     // the area of the rectangle is equal to 6  
      assert r.getArea() == 6 : printError("area", r);  
      
            // Assert Length & Breadth  
      
     // From the code, the expected behavior is that   
     // the length should always be equal to 3 and  
     // the breadth should always be equal to 2  
      assert r.getLength() == 3 : printError("length", r);  
      
            assert r.getBreadth() == 2 : printError("breadth", r);  
      
        }  
      
        private String printError(String errorIdentifer, Rectangle r) {  
      
            return "Unexpected value of " + errorIdentifer + "  for instance of " + r.getClass().getName();  
      
        }  
      
        public static void main(String[] args) {  
      
            LSPDemo lsp = new LSPDemo();  
      
            // An instance of Rectangle is passed  
      
      lsp.calculateArea(new Rectangle());  
      
            // An instance of Square is passed  
      
      lsp.calculateArea(new Square());  
      
        }  
      
    }

### Java Code Samples to Illustrate the LSP


    class Bird {
      public void fly(){}
      public void eat(){}
    }
    class Crow extends Bird {}
    class Ostrich extends Bird{
      fly(){
        throw new UnsupportedOperationException();
      }
    }
     
    public BirdTest{
      public static void main(String[] args){
        List<Bird> birdList = new ArrayList<Bird>();
        birdList.add(new Bird());
        birdList.add(new Crow());
        birdList.add(new Ostrich());
        letTheBirdsFly ( birdList );
      }
      static void letTheBirdsFly ( List<Bird> birdList ){
        for ( Bird b : birdList ) {
          b.fly();
        }
      }
    }


What do you think would happen when this code is executed? As soon as an Ostrich instance is passed, it blows up!!! Here the sub type is not replaceable for the super type.

**How do we fix such issues?**

By using factoring. Sometimes factoring out the common features into a separate class can help in creating a hierarchy that confirms to LSP.

In the above scenario we can factor out the fly feature into- Flight and NonFlight birds.

    class Bird{
      public void eat(){}
    }
    class FlightBird extends Bird{
      public void fly()()
    }
    class NonFlight extends Bird{}


Interface Segregation Principle (ISP)
-------------

Interface Segregation Principle stats that, a client should not implement an interface if it doesn't use that. This happens mostly when one interface contains more than one functionality, and the client only needs one functionality and no other.  
  
Interface design is a tricky job because once you release your interface you can not change it without breaking all implementation.  

In our case, the Athlete interface is an interface with some actions of an athlete:

      
    public interface Athlete {
    
     void compete();
    
     void swim();
    
     void highJump();
    
     void longJump();

	}


We have added the method compete, but also there some extra methods like `swim,` `highJump` , and `longJump`.

Suppose that John Doe is a swimming athlete. By implementing the Athlete interface, we have to implement methods like `highJump` and `longJump`, which JohnDoe will never use.

We will follow the interface segregation principle and refactor the original interface:
Then we will create two other interfaces — one for Jumping athletes and one for Swimming athletes.

    public interface SwimmingAthlete extends Athlete {
    
     void swim();
    
    }
   
    public interface JumpingAthlete extends Athlete {
    
     void highJump();
    
     void longJump();
    
    }


----------

### Footnotes
-------------

[1] 

[2] 
