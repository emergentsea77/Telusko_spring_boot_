## 06 - Ref Attribute 

In Spring, the ref attribute is used in the <property> tag to assign reference-type values (i.e., objects of other beans) to a property. 

- The ref attribute allows one bean to refer to another bean within the Spring container. 

- The value of the ref attribute should be the id of another bean that you want to reference. 

- For the reference injection to work, the referenced bean must be defined in the configuration file. Otherwise, Spring will throw an error during the container initialization. 

## **Example:** 

## _**Alien.java**_ 

The Alien class has a Laptop object as a dependency. A setter method is used to inject this dependency. 

public class Alien { private int age; public Alien() { System.out.println("Object Created"); } public int getAge() { return age; } public void setAge(int age) {    // Setter Injection 

System.out.println("Setter called"); this.age = age; } public void code() { System.out.println("Coding"); } } 

## _**Laptop.java**_ 

A simple class with a compile() method. 

public class Laptop { public Laptop() { System.out.println("Laptop object created"); } } 

## _**Spring.xml**_ 

<bean id="alien1" class="com.telusko.Alien"> 

<property name="age" value="21"></property> <property name="lap" ref="lap1"></property> 

</bean> 

<bean id="lap1" class="com.telusko.Laptop"> 

</bean> 

Here, 

- The Alien bean (alien1) has a Laptop bean (lap1) injected into its lap property using the ref attribute. 

- The name="lap" corresponds to the lap property in the Alien class, and ref="lap1" points to the bean with ID lap1. 

## _**App.java**_ 

public class App { 

public static void main( String[] args ) { 

ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml"); 

Alien obj1 = (Alien) context.getBean("alien1"); 

System.out.println(obj1.getAge()); obj1.code(); 

} } 

## _**Output:**_ 

- ➢ If there are multiple beans of the same class, Spring differentiates them using the id attribute. 

- ➢ Only the bean with the id specified in the ref attribute will be injected. 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.6%20Ref%20Attribute/Spring1 

