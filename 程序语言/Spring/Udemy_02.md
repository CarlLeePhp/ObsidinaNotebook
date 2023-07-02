From 19 to 28

## Multi-Module Project

#### Benefits of a multi-module project

+ When you are working on new functionality or bug fixes for a certain part of the project, you can simply focus on that module and run just the tests for that module, compiling a fraction of the entire project code and running just the related tests. This speeds up development time.
+ You  can re-use the code from modules across difference projects.



#### UML

For more info visit https://www.uml-diagrams.org



#### Project Setting

The parent project do not need source code, so we can delete that folder.

Part of the pom.xml of parent project: 

```xml
<packaging>pom</packaging>

<properties>
    <logback.version>1.2.3</logback.version>
    <spring.version>5.1.4.RELEASE</spring.version>
    <java.version>11</java.version>
</properties>

<dependencyManagement>
    <dependencies>
        <!-- logback-classic -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>${logback.version}</version>
        </dependency>

        <!-- spring-context -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>

    </dependencies>
</dependencyManagement>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.0</version>
            <configuration>
                <target>${java.version}</target>
                <source>${java.version}</source>
                <release>${java.version}</release>
            </configuration>
        </plugin>
    </plugins>
</build>
```



Part of the core module:

```xml
<dependencies>
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
    </dependency>
</dependencies>
```



#### Using a Spring Container

beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="numberGenerator" class="academy.learnprogramming.NumberGeneratorImpl" />

</beans>
```



#### 24. Constructor based Dependency Injection (DI)

Create a constructor in the GameImpl class

```java
public GameImpl (NumberGenerator numberGenerator) {
    this.numberGenerator = numberGenerator;
}
```



beans.xml. The ref="numberGenerator" is come from the ID of the bean above.

```xml
<bean id="numberGenerator" class="academy.learnprogramming.NumberGeneratorImpl" />

<bean id="game" class="academy.learnprogramming.GameImpl">
    <constructor-arg ref="numberGenerator" />
</bean>
```



Call reset from the main method:

```java
// get game bean from context (container)
    Game game = context.getBean(Game.class);
    game.reset();
```



#### 25. Setter based Dependency Injection

Add a set for a variable.

```java
public void setNumberGenerator(NumberGenerator numberGenerator) {
    this.numberGenerator = numberGenerator;
}
```



Then set the beans.xml. The name in property is a variable of the class GameImpl. The ref is a ID of a bean.

```xml
<bean id="numberGenerator" class="academy.learnprogramming.NumberGeneratorImpl" />

<bean id="game" class="academy.learnprogramming.GameImpl">
    <property name="numberGenerator" ref="numberGenerator" />
</bean>
```



Call reset from the main method:

```java
// get game bean from context (container)
    Game game = context.getBean(Game.class);
    game.reset();
```



#### 25. Setter or Constructor Based DI

xxx

+ One benefit of setter injection is that setter methods make objects of that class amenable to reconfiguration or re-injection later.

Dependency Resolution Process

The container performs bean dependency resolution as follows:

+ The ApplicationContext is created and initialized with configuration metadata that describes all the beans (configuration can be implemented using XML or with Annotations via Java code)
+ For each bean, its dependencies are expressed in the form properties or constructor arguments.
+ These dependencies are provided to the bean, When the bean ...

#### 26. Bean lifecycle Call backs

Or set in the xml file without call the reset method. Delete the "game.reset();" from main method.

```xml
<bean id="game" class="academy.learnprogramming.GameImpl" init-method="reset">
    <property name="numberGenerator" ref="numberGenerator" />
</bean>
```



#### 27. XML or Annotation

**XML Based Configurations - Pros**







