## 05 - Setter Injection 

Setter Injection is a way in Spring for injecting dependencies or values into a bean through its setter methods. 

- Inside the <bean> tag, the <property> tag is used to inject values into the corresponding fields of the bean via its setter methods. 

   - **name** : Refers to the name of the property (variable) in the class. 

   - **value** : Assigns the value to that property. 

- The value attribute in the <property> tag is used to inject primitive types such as int, boolean, String, etc. 

- It is commonly used when the bean has optional or configurable properties. 

## **Code:** 

_**Alien.java**_ 

private int age; 

public Alien() { 

System.out.println("Object Created"); 

} 

public int getAge() { 

return age; 

} 

public void setAge(int age) {    // Setter Injection 

System.out.println("Setter called"); this.age = age; 

} 

public void code() { 

System.out.println("Coding"); } 

_**App.java:**_ 

public class Alien { private int age; public Alien() { System.out.println("Object Created"); } public int getAge() { return age; } public void setAge(int age) { System.out.println("Setter called"); this.age = age; } public void code() { System.out.println("Coding"); } } 

## _**Spring.xml**_ 

<bean id="alien1" class="com.telusko.Alien" > 

<property name="age" value="21"> </property> </bean> 

- The name="age" corresponds to the age variable in the Alien class. 

- The value="21" assigns the value 21 to the age variable. 

## _**Output:**_ 

In this example, When the ApplicationContext loads the XML file, it creates an object for the Alien class. The setter method setAge(int age) is called, and the value 21 is passed as an argument. 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.5%20Setter%20Injection/Spring1 

