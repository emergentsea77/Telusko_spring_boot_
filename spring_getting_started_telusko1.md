## **Autowiring** 

**Autowiring** is a feature in the Spring Framework that allows the Spring container to automatically inject dependencies into a bean. It simplifies the process of wiring together beans by eliminating the need for explicit setter or constructor calls. When a bean requires a dependency, Spring resolves and injects it into the bean automatically. 

## **1. Main Application Class (SpringBootDemoApplication)** 

This class starts the Spring Boot application and retrieves the Alien bean from the Spring context. 

package com.telusko.app; 

import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication; import org.springframework.context.ApplicationContext; 

@SpringBootApplication public class SpringBootDemoApplication { public static void main(String[] args) { ApplicationContext context = SpringApplication.run(SpringBootDemoApplication.class, args); 

Alien obj = context.getBean(Alien.class); _// Retrieve Alien bean // Call method on Alien bean_ 

} } 

## **2. Alien Class (Alien.java)** 

This class represents a component that depends on a Laptop bean, which is injected automatically using the @Autowired annotation. 

package com.telusko.app; 

import org.springframework.beans.factory.annotation.Autowired; import org.springframework.stereotype.Component; 

@Component public class Alien { @Autowired Laptop laptop; _// Autowiring of Laptop bean_ 

public void code() { laptop.compile(); _// Calling Laptop's compile method_ } } 

## **3. Laptop Class (Laptop.java)** 

This is the class whose instance (bean) is injected into the Alien class. The compile method is called when the Alien object invokes its code() method. 

package com.telusko.app; 

import org.springframework.stereotype.Component; 

@Component 

public class Laptop { 

public void compile() { System.out.println("Compiling..."); _// Output message_ } } 

## **Output** 

When you run the SpringBootDemoApplication class, the Alien bean's code() method is called, which in turn calls the Laptop bean's compile() method. The output will be: 

Compiling... 

## **DI Using Spring Boot** 

## **Inversion of Control (IoC)** 

**Inversion of Control (IoC)** is a design principle where the control of object creation and management is transferred from the application code to a framework or container, allowing developers to focus on business logic rather than dependency management. 

## **Dependency Injection (DI)** 

**Dependency Injection (DI)** is a specific implementation of IoC that provides an object's dependencies from an external source, rather than having the object create them internally. This promotes loose coupling, making code more modular, testable, and maintainable. 

**Step 1: Without Spring (Basic Java Implementation)** 

public class Alien { public void code() { System.out.println("Coding"); } } 

- The Alien class has a simple method code() that prints "Coding". 

## **Step 2: Main Class without Spring** 

public class SpringBootDemoApplication { public static void main(String[] args) { 

new Alien(); _// Manually creating the object_ 

} 

} 

- The Alien object is instantiated **manually** and the method code() is called. 

## **Output:** 

Coding 

## **Step 3: Using Spring Framework for Dependency Injection** 

1. Annotate the Alien class with @Component to let Spring manage it as a bean: 

@Component 

public class Alien { public void code() { System.out.println("Coding"); } } 

2. Update the main class to use **Spring’s ApplicationContext** to get the Alien bean: 

public class SpringBootDemoApplication { 

public static void main(String[] args) { 

ApplicationContext context = 

SpringApplication.run(SpringBootDemoApplication.class, args); 

Alien obj = context.getBean(Alien.class); _// Getting bean from Spring context_ 

} 

} 

## **Output:** 

## Coding 

- Now the Alien object is managed by Spring, not manually instantiated. 

## **Step 4: Multiple Bean Calls (Optional)** 

- You can call the Alien bean multiple times using context.getBean(): 

Alien obj1 = context.getBean(Alien.class); obj1.code(); 

Alien obj2 = context.getBean(Alien.class); obj2.code(); 

- Spring will manage the lifecycle and instantiation, making DI easier. 

## **Summary:** 

- **Step 1 & 2** : Manual object creation without Spring. 

- **Step 3** : Object creation is managed by Spring using @Component and ApplicationContext. 

TELUSKO 

## 01 - SPRING 1st PROJECT 

## **Steps to Setup a Maven Spring Project:** 

Create a new **Maven project** using your IDE or CLI. 

- **Project Name:** Assign a suitable name to the project (e.g., SpringDemo). 

- **Location:** Choose a directory to store your project. 

- **JDK Version:** Ensure **JDK 17** or higher is selected (required for Spring 6 framework). 

- **Catalog:** Select **Internal** as the catalog. 

- **Archetype:** Choose **QuickStart** to create the basic project structure. 

- **Version:** Set it to **1.1** . 

- **GroupId:** Represents the project's root package (e.g., com.telusko). 

- **ArtifactId:** The project's name (e.g., spring-app). 

- **Version:** Usually set to **1.0-SNAPSHOT** . 

- ➢ Once the Maven project is created, the pom.xml file should include basic dependencies and configurations. 

- ➢ Verify the project structure by running the App.java file. You should see "Build Success" if the project is correctly set up. 

## **IOC (Inversion of Control) Container:** 

- The IOC Container in Spring is responsible for managing the lifecycle of objects (called beans), their configurations, and their dependencies. 

- It inverts the control of object creation from the developer to the framework. 

- IOC container also injects the necessary dependencies. 

- The two key types of IOC containers in Spring are: 

   - BeanFactory: A basic container for managing beans. 

- ApplicationContext: A more feature-rich container that builds upon BeanFactory. 

## 👉 **BeanFactory Interface:** 

- ➢ BeanFactory is a lightweight container in Spring that provides basic DI and bean management functionalities. 

- ➢ It follows the l **azy loading principle** , meaning beans are only created when requested 

## 👉 **ApplicationContext Interface:** 

ApplicationContext is an advanced IOC container in Spring. It builds on top of BeanFactory and provides additional features like: 

- ➢ **Event propagation** : Handles events published by beans. 

- ➢ **AOP (Aspect-Oriented Programming)** : Supports declarative AOP features. 

- ➢ **Message resource handling** : Allows support for internationalization and easy access to resource bundles. 

- ➢ **Bean Autowiring** : Automatic injection of dependencies based on bean types. 

- ➢ **Different Context Types** : Provides several specialized types of ApplicationContext implementations, such as: 

   - **ClassPathXmlApplicationContext** : Loads context from an XML file located in the classpath. 

- **FileSystemXmlApplicationContext** : Loads context from an XML file 

   - outside the classpath. 

- **AnnotationConfigApplicationContext** : Supports Java-based configuration without XML. 

## **Adding Spring Context Dependency:** 

To use the ApplicationContext, add the **spring-context** dependency in pom.xml 

## Website Link: https://mvnrepository.com/ 

**Dependency:** 

- _<!-- https://mvnrepository.com/artifact/org.springframework/spring-context --> <dependency>_ 

_<groupId>org.springframework</groupId>_ 

_<artifactId>spring-context</artifactId>_ 

_<version>6.1.12</version>_ 

_</dependency>_ 

## 👉 **XML-Based Configuration with ClassPathXmlApplicationContext:** 

You need to use ClassPathXmlApplicationContext to load bean definitions from an XML configuration file. 

## **Example code to create a Spring container:** 

ApplicationContext context = new ClassPathXmlApplicationContext(); Alien obj = (Alien)context.getBean("alien"); obj.code(); 

- ApplicationContext -> manages the lifecycle and configuration of Spring beans. 

- ClassPathXmlApplicationContext ->  loads the bean configuration from an XML file located on the classpath 

- getBean() -> method fetches a bean with the specified id (in this case, "alien") from the IOC container. It returns an object of type Object, so explicit casting is required to convert it to the type of the desired bean 

- Alien obj = (Alien) -> ensures that the returned bean is treated as an object of the Alien class 

- obj.code() ->  calls the code() method on the Alien object 

## 👉 **Common Error: BeanFactory Not Initialized** 

The error occurs when accessing a bean before the Spring context is properly initialized. The Spring container (ApplicationContext) is not fully loaded or closed. 

## **Error:** 

Exception in thread "main" java.lang.IllegalStateException: BeanFactory not initialized or already closed - call 'refresh' before accessing beans via the ApplicationContext at 

org.springframework.context.support.AbstractRefreshableApplicationContext.getB eanFactory(AbstractRefreshableApplicationContext.java:169)at org.springframework.context.support.AbstractApplicationContext.getBean(Abstrac tApplicationContext.java:1243)at com.telusko.App.main(App.java:18) 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.1%20Spring%201st%20Project/Spring1 

## 02 - Spring Based Xml Config 

Spring Framework provides three main methods to create and manage objects within the application context: 

1. **XML Configuration** : Configuring beans using XML files. 

2. **Java-Based Configuration** : Configuring beans using Java classes. 

3. **Annotations** : Configuring beans using annotations directly in the code 

## **Steps for XML-Based Spring Configuration:** 

## **1. Create XML Configuration file:** 

- Create an XML configuration file in the **src/main/resources** directory. This 

- file will define the beans that the Spring container will manage. 

- e.g., Spring.xml file in the src/main/resources 

## 2. **Define Beans in XML:** 

- ⭐ `Beans` are objects that form the backbone of a Spring application. They are managed by the Spring IoC (Inversion of Control) container. 

Each bean is defined using the **<bean>** tag in the XML configuration file. 

- **id** : A unique identifier for the bean, which is used to reference it. 

- **class** : The fully qualified class name of the bean. 

**Example** : 

<bean id="alien" class="com.telusko.Alien"> 

</bean> 

## 3. **Define XML Configuration Structure** : 

Use the <beans> root element. It specifies the XML namespace and schema definitions required for bean configuration. 

**Website Link:** https://docs.spring.io/spring-framework/docs/4.2.x/springframework-reference/html/xsd-configuration.html 

## **XML Schema:** 

_<?xml version="1.0" encoding="UTF-8"?>_ 

_<beans xmlns="http://www.springframework.org/schema/beans"_ 

_xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"_ 

_xmlns:util="http://www.springframework.org/schema/util"_ 

_xsi:schemaLocation="_ 

_http://www.springframework.org/schema/beans_ 

_http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util_ 

_http://www.springframework.org/schema/util/spring-util.xsd"> <!-- bean definitions here -->_ 

_</beans>_ 

**Code:** 

## _**App.java**_ 

## _**Alien.java**_ 

## _**Spring.xml**_ 

## _**Output:**_ 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.2%20Spring%20Bean%20Xml%20Config/Spring1 

## 03 - Object Creation 

ApplicationContext is the central interface to the Spring IoC container. 

- It is used to load the Spring XML configuration file and create objects (beans) defined within it. 

- When the ApplicationContext is instantiated, it automatically reads the XML configuration file, creates the container, and instantiates all the beans defined in it. 

- Every time a bean is created, the Spring container calls the constructor of the corresponding class, initializing the object. 

## **Workflow Example:** 

- Use ClassPathXmlApplicationContext to load the XML configuration file, which sets up the Spring container and creates the beans defined within the <bean> tag. 

ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml"); 

- Use the getBean() method to retrieve an object from the container and get its reference. This method returns the object based on the bean’s ID specified in the XML file. 

Alien obj = (Alien) context.getBean("alien"); pt Here, the bean with ID alien is retrieved, and a reference to the Alien object is obtained. 

- After retrieving the bean, we can call its methods with any object in Java. 

obj.code(); pt 

## **Multiple Beans Creation** : 

The number of beans defined in the XML file corresponds to the number of objects created when the ApplicationContext is initialized. 

<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.springframework.org/schema/bean http://www.springframework.org/schema/beans/spring-beans.xsd"> 

<!-- Bean Definitions --> <bean id="alien1" class="com.telusko.Alien"> </bean> 

<bean id="alien2" class="com.telusko.Alien"> </bean> <bean id="lap" class="com.telusko.Laptop"> </bean> </beans> 

- Two objects of the Alien class (alien1 and alien2) will be created. 

- One object of the Laptop class (lap) will be created. 

- Both alien1 and alien2 are **distinct objects** , allowing to work with multiple instances of the Alien class independently. 

- ➢ By defining multiple beans in the XML file, we can create and manage multiple objects of the same class with different IDs. 

## **Output:** 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.3%20Object%20Creation/Spring1 

## 04 - Scopes 

In Spring, beans can have different scopes that define how many instances of the bean are created and how they are shared across the application. 

## 👉 **Types of Bean Scopes:** 

## 1. **Singleton** (Default Scope): 

- In the Singleton scope, only one instance of the bean is created, even if there are multiple references to it. 

- Every time we retrieve the bean from the Spring container, we will get the same instance. 

## 2. **Prototype** : 

- In the Prototype scope, a new object is created each time when we call the getBean() method. 

- Each reference will point to a distinct instance of the bean. 

## 3. **Request** (for Spring Web): 

   - In the Request scope, a new bean instance is created for every HTTP request. This scope is available in web applications. 

4. **Session** (for Spring Web): 

   - In the Session scope, a new bean instance is created for every HTTP session. This scope is specific to web applications. 

⭐ `In Spring, beans are` **Singleton by default** . This means that only one instance of the bean is created and shared across the entire application context. 

## **Example:** 

## _**App.java**_ 

public class App { public static void main( String[] args ) { 

ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");  // create a container Alien obj1 = (Alien) context.getBean("alien1"); obj1.age = 21; System.out.println(obj1.age); Alien obj2 = (Alien) context.getBean("alien1"); System.out.println(obj2.age); } } 

## _**Alien.java**_ 

int age; public Alien() { System.out.println("Object Created"); } public void code() { System.out.println("Coding"); } 

## _**Spring.xml**_ 

<bean id="alien1" class="com.telusko.Alien"> </bean> <bean id="lap" class="com.telusko.Laptop"> </bean> 

## _**Output:**_ 

## **Changing the Scope in XML:** 

We can explicitly define the scope of a bean using the scope attribute in the <bean> tag. 

## **Singleton:** 

<bean id="alien1" class="com.telusko.Alien" /> 

**Or** 

<bean id="alien1" class="com.telusko.Alien" scope="singleton" /> 

- In this case, the alien1 bean will be Singleton by default. 

## **Prototype:** 

<bean id="alien1" class="com.telusko.Alien" scope="prototype" /> 

- Here, alien1 bean is defined with a prototype scope. 

- In this, a new object will be created for each call to getBean() 

- ➢ The **Prototype scope** is useful when we need a new instance of the bean for each operation, such as in multi-threaded environments, or when dealing with stateless objects that require frequent instantiation. 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 

course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.4%20Scopes/Spring1 

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

## 07 - Constructor Injection 

Constructor Injection is used in Spring when we want to inject values or dependencies into a bean during its creation. 

- It is useful when the values or objects must be provided during object initialization. 

- In Constructor Injection, values and references are passed to the bean through its constructor. 

- Spring offers the **<constructor-arg>** tag to handle this injection. 

- <constructor-arg> Tag includes: 

■ **value** : Used to pass primitive values. 

■ **ref** : Used to pass references to other beans. 

- The order and type of arguments must match the constructor’s parameters. 

## **Example:** 

## _**Alien.java**_ 

The class takes an age (primitive) and a Laptop object as parameters in its constructor. 

public class Alien { 

private int age; 

//private Laptop lap = new Laptop(); 

private Laptop lap; 

private int salary; 

public Alien() { 

System.out.println("Object Created"); } 

@ConstructorProperties({"age","lap"}) public Alien(int age,Laptop lap) { System.out.println("Para Constructor Called"); this.age = age; this.lap = lap; } public void code() { System.out.println("Coding"); lap.compile(); } } 

## _**Laptop.java**_ 

public class Laptop { public Laptop() { System.out.println("Laptop object created"); } public void compile() { System.out.println("Compiling"); } } 

## _**Spring.xml**_ 

<bean id="alien1" class="com.telusko.Alien" > 

<constructor-arg value="21"></constructor-arg> <constructor-arg ref="lap1"></constructor-arg> </bean> <bean id="lap1" class="com.telusko.Laptop"> </bean> 

Here, 

- value="21": Injects the age value (primitive) into the constructor. 

- ref="lap1": Injects the reference to the Laptop bean. 

## _**App.java**_ 

public class App { 

public static void main( String[] args ) { 

ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml"); 

Alien obj1 = (Alien) context.getBean("alien1"); System.out.println(obj1.getAge()); 

obj1.code(); 

} } 

## _**Output:**_ 

## **Handling Argument Types and Indexes:** 

- **Type Attribute** : When arguments are of different types, the type attribute can be used to specify the exact type of the argument. 

<constructor-arg type="int" value="21"/> <constructor-arg type="com.telusko.Laptop" ref="lap1"/> 

- **Index Attribute** : In some cases, the constructor parameters may be of the same type. The index attribute specifies the 0-based index of the argument. 

<constructor-arg index="0" value="21"/> <constructor-arg index="1" ref="lap1"/> 

- **Name Attribute** : If the constructor parameters have names, the name attribute can be used. It must still follow the order of the parameters unless the @ConstructorProperties annotation is used. 

<constructor-arg name="age" value="21"/> 

<constructor-arg name="lap" ref="lap1"/> 

## 👉 **Using @ConstructorProperties Annotation** 

- ➢ If the parameters are not provided in sequence using the name attribute, you can use the @ConstructorProperties annotation to specify the exact names of the constructor arguments. 

- ➢ This annotation helps Spring map the arguments to the constructor parameters by name, even if the values are provided in a different order in the XML file. 

@ConstructorProperties({"age", "lap"}) public Alien(int age, Laptop lap) { this.age = age; this.lap = lap; } 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.7%20Constructor%20Injection/Spring1 

## 08 - Creating Interface 

In Spring, interfaces are often used to achieve loose coupling between components, allowing for flexible design and easy substitution of implementations. 

- An interface defines a set of methods that implementing classes must provide. 

- Spring can inject different implementations of the same interface based on the configuration. 

- Different classes can implement the same interface. 

- We can switch between implementations by specifying which one to inject in the Spring configuration. 

## **Example:** 

## _**Computer.java**_ 

This interface declares a method compile(), which both Laptop and Desktop classes will implement. 

public interface Computer { void compile(); } 

## _**Laptop.java**_ 

Implements the Computer interface and provides the compile() method. 

public class Laptop implements Computer { public void compile() { System.out.println("Compiling using Laptop"); } } 

## _**Desktop.java**_ 

Another implementation of the Computer interface with its own compile() method. 

public class Desktop implements Computer { 

public void compile() { System.out.println("Compiling using Desktop"); } } 

## _**Alien.java**_ 

The Alien class has a dependency on the Computer interface, and it can work with any implementation of Computer. 

public class Alien { private int age; private Computer comp; public Alien() { System.out.println("Object Created"); } public int getAge() { return age; } public void setAge(int age) {    // Setter Injection System.out.println("Setter called"); this.age = age; } public Computer getComp() { return comp; } public void setComp(Computer comp) { 

this.comp = comp; } public void code() { System.out.println("Coding"); comp.compile(); } } 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.8%20Creating%20Interface/Spring1 

## 09 - Autowiring 

Autowiring is a mechanism used by Spring to inject dependencies into beans automatically. 

_**Wiring**_ refers to connecting beans by specifying dependencies. It is done by manually specifying references using the ref attribute in XML. 

_**Autowiring**_ allows Spring to automatically inject dependencies by analyzing the bean's name or type, without requiring explicit ref properties in the XML configuration. 

Spring provides multiple autowiring modes: 

- **byName** : Autowires the bean by matching the property name with the bean id. 

- **byType** : Autowires the bean by matching the property type with the bean type. 

- **constructor** : Autowires the bean via constructor injection. 

- **autodetect** : Tries constructor first, then falls back to byType. 

## **Autowiring by Name:** 

In **byName** autowiring, Spring looks for a bean in the container with the same name as the property. If such a bean is found, Spring injects it automatically. 

## **Example:** 

<bean id="alien1" class="com.telusko.Alien" autowire="byName"> <property name="age" value="21" /> <!--  <property name="comp" ref="lap1" /> --> </bean> 

<bean id="comp" class="com.telusko.Laptop"></bean> 

- Here, the Alien bean depends on the Computer interface. In the Alien class, there is a comp property. Spring will automatically wire the Laptop bean because it has an id of comp, which matches the property name. 

## _**Output:**_ 

⭐ `If we explicitly specify a property in the bean definition, Spring will prioritize this over the autowiring mechanism.` 

<bean id="alien1" class="com.telusko.Alien" autowire="byName"> <property name="age" value="21" /> <property name="comp" ref="comp1" /> </bean> <bean id="comp" class="com.telusko.Laptop"></bean> <bean id="comp1" class="com.telusko.Desktop"></bean> 

## _**Output:**_ 

## **Autowiring by Type:** 

In **byType** autowiring, Spring looks for a bean with a type that matches the property type in the dependent bean. If such a bean is found, it is injected automatically. 

## **Example:** 

<bean id="alien1" class="com.telusko.Alien" autowire="byType"> 

<property name="age" value="21" /> 

</bean> 

<bean id="comp" class="com.telusko.Laptop"></bean> 

- In this,  Spring injects the Laptop bean into the comp property because the Laptop class implements the Computer interface, and the comp property in the Alien class is of type Computer. 

## _**Output:**_ 

⭐ `If there are multiple beans of the same type in the Spring container, autowiring by type will cause a conflict, and Spring will throw an error. To resolve this, we can switch to` **byName** autowiring, or primary bean, or provide an explicit reference. 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.9%20Autowiring/Spring1 

## 10 - Primary Bean 

In Spring, when autowiring beans by type, conflicts can arise if multiple beans of the same type exist in the Spring container. Spring will be unable to determine which bean to inject and will throw an error. 

To resolve these conflicts, Spring allows marking one of the beans as **primary** , which means that Spring will prefer this bean when performing autowiring. 

- The **primary** attribute can be set to **true** on one of the beans of the same type. This marks the bean as the default choice for autowiring by type, giving it preference over other beans of the same type. 

- The primary bean is injected automatically unless we explicitly specify a different bean using the ref attribute in the XML configuration. 

## **Example:** 

<bean id="alien1" class="com.telusko.Alien" autowire="byType"> <property name="age" value="21" /> </bean> 

<bean id="comp" class="com.telusko.Laptop" primary="true"></bean> <bean id="comp1" class="com.telusko.Desktop"></bean> 

- Since both Laptop and Desktop beans implement the Computer interface, Spring would face a conflict when autowiring by type. 

- However, by marking the Laptop bean as **primary** , Spring resolves the conflict and autowires the Laptop bean into the Alien class. 

## _**Output:**_ 

⭐ `If we explicitly specify a reference to a bean, Spring will inject that bean, even if another bean is marked as primary. This allows us to manually control which bean is injected when needed.` 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.10%20Primary%20Bean/Spring1 

## 11 - Lazy Init Bean 

By default, when the Spring container is initialized, all beans are created eagerly. The container will create and manage all beans when the application context is loaded. 

ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml"); 

All beans mentioned in the XML file are created immediately, even if they are not used. 

## **Lazy Initialization:** 

Lazy loading, or lazy initialization, refers to a design pattern in which the initialization of an object is deferred until it is actually needed, rather than initializing it at the time of application startup. 

- By marking a bean with the lazy-init="true" attribute, Spring delays the creation of the bean until it is needed. Spring will only create the bean when you call getBean(), which improves startup time. 

- Even when a bean is lazily initialized, it is still a singleton by default. 

- Once the lazy bean is created, it remains in the Spring container and will be reused on subsequent calls. 

## **Example:** 

<bean id="alien1" class="com.telusko.Alien" autowire="byType"> 

<property name="age" value="21" /> 

</bean> 

<bean id="comp" class="com.telusko.Laptop" primary="true"></bean> 

<bean id="comp1" class="com.telusko.Desktop" lazy-init="true"></bean> 

Here, 

- The Alien and Laptop beans will be eagerly initialized when the application context is created. 

- The Desktop bean is lazy-initialized and we have to use this to create the object of it. 

## _**Output:**_ 

After calling the bean, it will create the object. 

Desktop obj = (Desktop) context.getBean("comp1"); 

_**Output:**_ 

⭐ `If an eagerly initialized bean depends on a lazyinitialized bean, the lazy bean will be created when the eager bean is created. This ensures that all required dependencies are available when the eager bean is constructed.` 

<bean id="alien1" class="com.telusko.Alien" autowire="byType"> 

<property name="age" value="21" /> 

<property name="comp" ref="comp1" /> 

</bean> <bean id="comp" class="com.telusko.Laptop" primary="true"> </bean> <bean id="comp1" class="com.telusko.Desktop" lazy-init="true"> </bean> 

## _**Output:**_ 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.11%20Lazy%20Init%20Bean/Spring1 

## 13 - Inner Bean 

In Spring, inner beans are beans defined inside another bean. This is useful when the inner bean is intended to be used only within the outer bean and doesn't need to be shared elsewhere. 

Inner beans are generally used when the object is private to the outer bean and is not reused anywhere else in the application context. 

## 👉 **Key Features of Inner Beans:** 

- **Scoped within the outer bean:** The inner bean is available only to the outer bean and can't be accessed or injected into any other beans. 

- **No need for an id:** While defining the inner bean, the id is not mandatory as it cannot be accessed outside the outer bean. 

- **Lifecycle:** The inner bean will be created and destroyed along with the outer bean. It will have the same lifecycle as the outer bean. 

## **Example:** 

<!-- Outer Bean --> 

<bean id="alien1" class="com.telusko.Alien"> 

<property name="age" value="21" /> 

<!-- Inner Bean --> 

<property name="comp"> 

<bean class="com.telusko.Laptop" /> 

</property> </bean> </beans> 

- Outer Bean (Alien): The Alien class has a property comp of type Laptop, which is injected with the inner bean. 

- Inner Bean (Laptop): This inner bean is defined inside the <property> tag for comp and provides an instance of the Laptop class. It will be created only when the outer bean (Alien) is instantiated. 

## **Code Link:** 

- https://github.com/navinreddy20/spring6 course/tree/c6690e4f2c70d8f530d70623f13d14ff0ffd7e7d/2%20Exploring%20Spri ng%20Framework/2.13%20InnerBean/Spring1 

## **- Java Based Configuration** 

Java-based configuration in Spring allows us to configure beans using Java classes instead of traditional XML configuration. 

## **Steps:** 

1.    Create a class annotated with @Configuration. This class will contain methods that return instances of the beans you need. 

2.    Use AnnotationConfigApplicationContext to initialize the Spring container and provide it with the configuration class. 

3.    Retrieve beans from the container using context.getBean(). 

## **Configuration Class:** 

import org.springframework.context.ApplicationContext; import 

org.springframework.context.annotation.AnnotationConfigApplicationContext; import org.springframework.context.annotation.Bean; 

import org.springframework.context.annotation.Configuration; 

_// Configuration class_ 

@Configuration public class AppConfig { 

@Bean public Desktop desktop() { return new Desktop(); } 

} 

## **Bean Class:** 

_// Bean class_ 

class Desktop { public Desktop() { 

System.out.println("Desktop Object Created"); } 

public void compile() { System.out.println("Compiling using Desktop"); 

} 

} 

## **Main Class:** 

_// Main class to test the configuration_ 

public class App { 

public static void main(String[] args) { ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class); 

_// Retrieve the Desktop bean from the context_ Desktop dt = context.getBean(Desktop.class); dt.compile(); _// Output: "Compiling using Desktop"_ 

} 

} 

## **Key Points:** 

- **@Configuration** : Marks the class as a source of bean definitions. 

- **@Bean** : Defines a bean, and the method name (desktop) becomes the bean name by default. 

- **AnnotationConfigApplicationContext** : Initializes the Spring context with the provided configuration class. 

## **Bean Name** 

When creating beans using @Bean, Spring assigns a default bean name as the method name. However, you can customize this name by providing a custom name using the name attribute in @Bean. 

## **Steps:** 

1. The default bean name is the name of the method that defines the bean. 

2.  To change the default name, you can use the @Bean(name = 

   - "customName") annotation. 

## **Configuration class:** 

@Configuration public class AppConfig { 

_// Default name of the bean is "desktop"_ @Bean public Desktop desktop() { return new Desktop(); } 

_// Bean with multiple names_ @Bean(name = {"com2", "desktop1", "beast"}) public Desktop desktop2() { return new Desktop(); } 

} 

## **Main  Class:** 

_// Main class to retrieve the bean_ public class App { 

public static void main(String[] args) { ApplicationContext context = new 

AnnotationConfigApplicationContext(AppConfig.class); 

_// Retrieve bean using the default name_ Desktop dt1 = context.getBean("desktop", Desktop.class); dt1.compile(); _// Output: "Compiling using Desktop"_ 

_// Retrieve bean using custom names_ Desktop dt2 = context.getBean("desktop1", Desktop.class); dt2.compile(); _// Output: "Compiling using Desktop"_ 

Desktop dt3 = context.getBean("beast", Desktop.class); dt3.compile(); _// Output: "Compiling using Desktop"_ } 

} 

## **Key Points:** 

- **Default Bean Name** : The method name (desktop). 

- **Custom Bean Name** : You can give a bean multiple names (com2, desktop1, beast), and it can be retrieved using any of those names. 

## **Scope** 

Spring beans have different scopes that define their lifecycle. The two most commonly used scopes are: 

- **Singleton** : (Default) Only one instance of the bean is created and shared across the application. 

- **Prototype** : A new instance of the bean is created every time it is requested. 

## **Steps:** 

1.    By default, Spring beans are singleton-scoped. 

2.    To change the scope, use the @Scope annotation and specify the scope type (e.g., "prototype"). 

## **Configuration class:** 

import org.springframework.context.annotation.Bean; import org.springframework.context.annotation.Configuration; import org.springframework.context.annotation.Scope; @Configuration public class AppConfig { _// Singleton scope (default)_ @Bean public Desktop desktopSingleton() { return new Desktop(); } 

_// Prototype scope (new instance each time)_ @Bean @Scope("prototype") public Desktop desktopPrototype() { 

return new Desktop(); 

} 

} 

## **Main Class:** 

_// Main class to demonstrate scope_ public class App { 

public static void main(String[] args) { ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class); 

_// Singleton scope_ Desktop dt1 = context.getBean("desktopSingleton", Desktop.class); Desktop dt2 = context.getBean("desktopSingleton", Desktop.class); System.out.println(dt1 == dt2); _// Output: true (Same instance)_ 

_// Prototype scope_ Desktop dt3 = context.getBean("desktopPrototype", Desktop.class); Desktop dt4 = context.getBean("desktopPrototype", Desktop.class); System.out.println(dt3 == dt4); _// Output: false (Different instances)_ } } 

## **Key Points:** 

- **Singleton Scope** : One shared instance for the entire application. 

- **Prototype Scope** : A new instance is created each time the bean is requested. 

TELUSKO 

## **Autowire** 

**Autowire** allows Spring to automatically resolve dependencies by type, injecting the appropriate beans into fields, constructors, or methods. 

## **Steps:** 

1.    Create a @Bean method in the configuration class. 

2.    Use @Autowired to automatically inject the dependency (in the constructor, field, or method). 

3.    In newer versions of Spring, the @Autowired annotation can be skipped as Spring performs automatic autowiring by type. 

There are several ways to perform autowiring in Spring: **field-level** , **setter-based** , and **constructor-based** injection. Each method has its use case and benefits. Here's a detailed explanation of each, along with the code examples. 

## **1. Field-Level Autowiring** 

**Field-level autowiring** is the simplest and most commonly used form of dependency injection. The dependency is injected directly into the field of the class using the @Autowired annotation. 

## **How it works:** 

- The @Autowired annotation is placed directly on the field. 

- Spring will automatically inject the appropriate bean by matching the type of the field with the bean. 

## **Example:** 

import org.springframework.beans.factory.annotation.Autowired; import org.springframework.context.annotation.Bean; import org.springframework.context.annotation.Configuration; import org.springframework.stereotype.Component; 

@Configuration public class AppConfig 

@Bean public Alien alien() { return new Alien(); } 

@Bean public Desktop desktop() { return new Desktop(); } } 

@Component class Alien { 

@Autowired _// Field-level Autowiring_ 

private Computer computer; _// Injected by Spring_ 

public void code() { System.out.println("Coding..."); 

computer.compile(); _// Calls the compile method of injected Computer_ } 

} 

interface Computer { void compile(); } 

@Component class Desktop implements Computer { @Override public void compile() { 

System.out.println("Compiling using Desktop"); } } 

_// Main class_ public class App { public static void main(String[] args) { ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class); Alien alien = context.getBean(Alien.class); alien.code(); _// Output: "Coding..." followed by "Compiling using Desktop"_ } } 

## **Key Points:** 

- **Pros** : Easy to use and clean code. 

- **Cons** : Less testable since the field is private, and you cannot pass dependencies through the constructor easily for testing. 

- **Use case** : Quick injection where testing flexibility is not a concern. 

## **2. Setter-Based Autowiring** 

**Setter-based autowiring** uses setter methods to inject dependencies into a class. It is a good option when you want to have some control over when the dependency is injected. 

## **How it works:** 

- The @Autowired annotation is placed on the setter method. 

- Spring calls the setter method to inject the dependency. 

## **Example:** 

@Component 

class Alien { 

private Computer computer; 

public void code() { System.out.println("Coding..."); 

computer.compile(); _// Calls the compile method of injected Computer_ } 

@Autowired _// Setter-based Autowiring_ public void setComputer(Computer computer) { this.computer = computer; } 

} 

_// Rest of the code remains the same as above_ 

## **Key Points:** 

- **Pros** : More flexibility and better for testing (you can inject mocks/stubs later). 

- **Cons** : Slightly more verbose than field injection. 

- **Use case** : When you need to perform additional logic before setting the dependency or if you want to make the dependency optional. 

## **3. Constructor-Based Autowiring** 

**Constructor-based autowiring** is considered the best practice by many developers. It ensures that the required dependencies are injected when the object is created, making the object immutable after construction. 

## **How it works:** 

- The @Autowired annotation is placed on the constructor. In Spring 4.3+, if a class has only one constructor, you can omit the @Autowired annotation. 

- Spring automatically injects the necessary dependencies into the constructor. 

## **Example:** 

@Component class Alien { 

private final Computer computer; 

_// Constructor-based Autowiring_ @Autowired public Alien(Computer computer) { 

this.computer = computer; _// Dependency injected through constructor_ } 

public void code() { System.out.println("Coding..."); 

computer.compile(); _// Calls the compile method of injected Computer_ } 

} 

_// Rest of the code remains the same as above_ 

## **Key Points:** 

- **Pros** : 

   - Enforces dependency injection at the time of object creation, making the object immutable. 

   - Makes the class easier to test by passing mock objects in the constructor. 

   - In newer versions of Spring, @Autowired can be omitted if the class has a single constructor. 

- **Cons** : Slightly more code to write, but it is the preferred method in many cases. 

- **Use case** : When you want to ensure immutability and the dependency is mandatory. 

TELUSKO 

## **Primary and  Qualifier** 

In some cases, there are multiple beans of the same type, and Spring does not know which bean to inject. This is where @Qualifier comes in. It allows you to specify which bean should be injected. 

## **Example with @Qualifier:** 

@Configuration public class AppConfig { @Bean public Desktop desktop() { return new Desktop(); } @Bean public Laptop laptop() { return new Laptop(); } } 

@Component class Alien { 

private Computer computer; 

_// Use @Qualifier to specify which bean to inject_ @Autowired @Qualifier("laptop") public Alien(Computer computer) { this.computer = computer; } public void code() { 

System.out.println("Coding..."); 

computer.compile(); _// Calls compile on the Laptop object_ 

} 

} 

@Component class Laptop implements Computer { @Override public void compile() { System.out.println("Compiling using Laptop"); } 

} 

@Component class Desktop implements Computer { @Override public void compile() { System.out.println("Compiling using Desktop"); 

} 

} 

_// Main class to demonstrate @Qualifier_ public class App { public static void main(String[] args) { ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class); 

_// Get the Alien bean_ Alien alien = context.getBean(Alien.class); alien.code(); _// Output: "Coding..." followed by "Compiling using Laptop"_ } 

} 

## **Key Points:** 

- **@Qualifier** : Used to resolve ambiguity when multiple beans of the same type exist. 

- **Example Output** : "Compiling using Laptop", as we specified to inject the Laptop bean using @Qualifier("laptop"). 

## **Using @Primary for Default Bean Injection** 

You can also use the @Primary annotation to specify the default bean that should be autowired when multiple candidates are present. 

## **Example with @Primary:** 

@Configuration public class AppConfig { @Bean @Primary _// This will be the default bean if no @Qualifier is specified_ public Laptop laptop() { return new Laptop(); } @Bean public Desktop desktop() { return new Desktop(); } } 

With this configuration, if no @Qualifier is used, Spring will inject the Laptop bean by default because of the @Primary annotation. 

## **Conclusion:** 

1. **Field-Level Autowiring** : The simplest, but can be harder to test due to private fields. 

2. **Setter-Based Autowiring** : More flexible and allows optional dependencies or pre-injection logic. 

3. **Constructor-Based Autowiring** : The most robust and preferred method for mandatory dependencies, enforcing immutability. 

4. **Autowiring with @Qualifier** : Used when multiple beans of the same type exist, to explicitly specify which one to inject. 

5. **Autowiring with @Primary** : Used to mark one bean as the default if multiple beans of the same type are present. 

## **Component Stereotype Annotations** 

## **1. What are Stereotype Annotations?** 

Stereotype annotations in Spring are specialized annotations that define and manage Spring Beans in the application context. These annotations assign specific roles to classes within the application, enabling Spring to detect and register them automatically as beans. 

## **2. Types of Stereotype Annotations** 

## 1. **@Component** : 

- General-purpose annotation to mark a class as a Spring-managed component. 

- Automatically registers the class as a bean when component scanning is enabled. 

Example: 

@Component 

public class Alien { public void code() { System.out.println("Alien is coding!"); } } 

## 2. **@Service** : 

- Specialization of @Component for the service layer. 

- Indicates a class containing business logic. 

## Example: 

@Service 

public class AlienService { public String assist() { return "Assistance provided by AlienService."; 

} 

} 

## 3. **@Repository** : 

- Specialization of @Component for the data access layer. 

- Indicates a class interacting with the database. 

Example: 

@Repository 

public class AlienRepository { public List<String> fetchAliens() { return List.of("Alien1", "Alien2"); } } 

## 4. **@Controller** : 

- Specialization of @Component for the presentation layer. 

- Handles HTTP requests in a Spring MVC application. 

Example: 

@Controller 

public class AlienController { @GetMapping("/alien") public String greet() { return "Greetings from Alien!"; } } 

## **3. The @Component Annotation** 

## ● **Purpose** : 

- Marks a class as a Spring component. 

- Simplifies bean creation and management. 

## ● **Key Features** : 

- Generic stereotype annotation for any Spring-managed component. 

- Automatically detected during component scanning. 

## **Example** : 

@Component public class Alien { public void code() { System.out.println("Alien is coding!"); } } 

## **4. @ComponentScan with @Configuration** 

## 1. **What is @ComponentScan?** 

- Specifies which packages Spring should scan for components, services, repositories, and controllers. 

- Detects and registers classes annotated with @Component, @Service, @Repository, and @Controller. 

## 2. **Use of @ComponentScan with @Configuration** : 

- Often used alongside @Configuration to specify the base packages for scanning. 

Example: 

@Configuration @ComponentScan("com.telusko") public class AppConfig { } 

## 3. **Explanation** : 

## ○ **@Configuration** : 

■ Indicates the class provides Spring configuration. 

## ○ **@ComponentScan("com.telusko")** : 

   - Scans the com.telusko package and sub-packages for stereotype annotations. 

- Ensures all annotated classes in the specified package are registered as beans. 

## **5. Advantages of Stereotype Annotations** 

## ● **Simplifies Configuration** : 

   - No need for explicit bean definitions in XML or Java-based configuration. 

- **Improves Readability** : 

   - Clarifies the role of a class in the application. 

- **Enables Component Scanning** : 

   - Automatically detects and registers beans, reducing boilerplate code. 

## **6. Practical Implementation** 

## 1. **Define Components** : 

- Create a class annotated with @Component. 

@Component public class Alien { public void code() { System.out.println("Alien is coding!"); } } 

## 2. **Set Up Configuration** : 

- Use @Configuration and @ComponentScan to enable component scanning. 

@Configuration @ComponentScan("com.telusko") public class AppConfig { 

} 

## 3. **Access Beans** : 

- Retrieve the bean from the Spring ApplicationContext. 

public class MainApp { 

public static void main(String[] args) { 

AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class); Alien alien = context.getBean(Alien.class); alien.code(); 

} } 

TELUSKO 

## **Autowire field, constructor, Setter** 

**Autowire** allows Spring to automatically resolve dependencies by type, injecting the appropriate beans into fields, constructors, or methods. 

## **Steps:** 

1.    Create a @Bean method in the configuration class. 

2.    Use @Autowired to automatically inject the dependency (in the constructor, field, or method). 

3.    In newer versions of Spring, the @Autowired annotation can be skipped as Spring performs automatic autowiring by type. 

There are several ways to perform autowiring in Spring: **field-level** , **setter-based** , and **constructor-based** injection. Each method has its use case and benefits. Here's a detailed explanation of each, along with the code examples. 

## **1. Field-Level Autowiring** 

**Field-level autowiring** is the simplest and most commonly used form of dependency injection. The dependency is injected directly into the field of the class using the @Autowired annotation. 

## **How it works:** 

- The @Autowired annotation is placed directly on the field. 

- Spring will automatically inject the appropriate bean by matching the type of the field with the bean. 

## **Example:** 

import org.springframework.beans.factory.annotation.Autowired; import org.springframework.context.annotation.Bean; import org.springframework.context.annotation.Configuration; 

import org.springframework.stereotype.Component; 

@Configuration public class AppConfig 

@Bean public Alien alien() { return new Alien(); } @Bean public Desktop desktop() { return new Desktop(); } 

} 

@Component class Alien { @Autowired _// Field-level Autowiring_ private Computer computer; _// Injected by Spring_ 

public void code() { "Coding..."); computer.compile(); _// Calls the compile method of injected Computer_ } 

} 

interface Computer { void compile(); } 

@Component class Desktop implements Computer { @Override 

public void compile() { System.out.println("Compiling using Desktop"); 

} 

} 

_// Main class_ public class App { public static void main(String[] args) { ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class); 

Alien alien = context.getBean(Alien.class); alien.code(); _// Output: "Coding..." followed by "Compiling using Desktop"_ } } 

## **Key Points:** 

- **Pros** : Easy to use and clean code. 

- **Cons** : Less testable since the field is private, and you cannot pass dependencies through the constructor easily for testing. 

- **Use case** : Quick injection where testing flexibility is not a concern. 

## **2. Setter-Based Autowiring** 

**Setter-based autowiring** uses setter methods to inject dependencies into a class. It is a good option when you want to have some control over when the dependency is injected. 

## **How it works:** 

- The @Autowired annotation is placed on the setter method. 

- Spring calls the setter method to inject the dependency. 

## **Example:** 

@Component class Alien { private Computer computer; 

public void code() { System.out.println("Coding..."); 

computer.compile(); _// Calls the compile method of injected Computer_ } 

@Autowired _// Setter-based Autowiring_ public void setComputer(Computer computer) { this.computer = computer; } 

} 

_// Rest of the code remains the same as above_ 

## **Key Points:** 

- **Pros** : More flexibility and better for testing (you can inject mocks/stubs later). 

- **Cons** : Slightly more verbose than field injection. 

- **Use case** : When you need to perform additional logic before setting the dependency or if you want to make the dependency optional. 

## **3. Constructor-Based Autowiring** 

**Constructor-based autowiring** is considered the best practice by many developers. It ensures that the required dependencies are injected when the object is created, making the object immutable after construction. 

## **How it works:** 

- The @Autowired annotation is placed on the constructor. In Spring 4.3+, if a class has only one constructor, you can omit the @Autowired annotation. 

- Spring automatically injects the necessary dependencies into the constructor. 

## **Example:** 

@Component class Alien { 

private final Computer computer; 

_// Constructor-based Autowiring_ @Autowired public Alien(Computer computer) { 

this.computer = computer; _// Dependency injected through constructor_ } 

public void code() { System.out.println("Coding..."); computer.compile(); _// Calls the compile method of injected Computer_ } 

} 

_// Rest of the code remains the same as above_ 

## **Key Points:** 

- **Pros** : 

   - Enforces dependency injection at the time of object creation, making the object immutable. 

   - Makes the class easier to test by passing mock objects in the constructor. 

   - In newer versions of Spring, @Autowired can be omitted if the class has a single constructor. 

- **Cons** : Slightly more code to write, but it is the preferred method in many cases. 

- **Use case** : When you want to ensure immutability and the dependency is mandatory. 

## **Primary Annotation** 

## **Using @Primary for Default Bean Injection** 

You can also use the @Primary annotation to specify the default bean that should be autowired when multiple candidates are present. 

## **Example with @Primary:** 

@Configuration public class AppConfig { @Bean @Primary _// This will be the default bean if no @Qualifier is specified_ public Laptop laptop() { return new Laptop(); } @Bean public Desktop desktop() { return new Desktop(); } } 

With this configuration, if no @Qualifier is used, Spring will inject the Laptop bean by default because of the @Primary annotation. 

**Note:** What happen if we are using @Primary and @Qualifier Qualifier has more precedence over primary 

## **Scope and Value Annotations** 

## **1. Scope Annotation (@Scope)** 

## ● **Purpose** : 

Specifies the lifecycle and scope of a bean in a Spring application. The default scope in Spring is **singleton** , which means only one instance of the bean is created for the application context. 

- **Usage** : 

   - @Scope("prototype"): Creates a new instance of the bean every time it is requested. 

   - Other scopes: singleton (default), request, session, application, etc. 

## **Example** : 

`@Component @Primary @Scope("prototype") public class Desktop implements Computer { public Desktop() { System.out.println("Desktop Object Created.."); }` 

`@Override public void compile() { System.out.println("Compiling using Desktop"); } }` 

## ○ **Explanation** : 

- The @Scope("prototype") ensures that a **new instance of Desktop** is created every time it is injected or retrieved from the Spring context. 

- The @Primary annotation marks this as the default bean for injection when there are multiple implementations of the Computer interface. 

## **2. Value Annotation (@Value)** 

## ● **Purpose** : 

Used to inject a specific value into a field, method parameter, or constructor. It can be used to set default values, read values from property files, or inject constant values. 

- **Usage** : 

   - Can inject literals, expressions, or property values. 

   - Format: @Value("value"). 

## **Example** : 

`@Component public class Alien { @Value("21") private int age;` 

`private Computer com;` 

`public Alien() { System.out.println("Alien Object Created"); } }` 

## ○ **Explanation** : 

- The @Value("21") injects the value 21 into the age field of the Alien class. 

- The Alien bean will always have age set to 21 unless overridden by external configuration. 

## **Key Points to Remember** 

## 1. **@Scope("prototype")** : 

   - Creates a new instance of the bean for every request. 

   - Useful for beans with independent state for each use. 

2. **@Value** : 

   - Injects values directly into fields. 

   - Can read values from property files or inject hardcoded constants. 

## 3. **Practical Usage** : 

- Use @Scope("prototype") for beans where state isolation is required. 

- Use @Value for initializing fields with constant or configurable values. 

