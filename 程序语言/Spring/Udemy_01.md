### Notes

Create a package under src.main.java folder.

Create a class under this package.



### Maven lifecycle

+ Maven build lifecycle. There are three built-in lifecycles: default, clean and site.



### Maven Plugins

+ "Maven" is really just a core framework of a collection of Maven Plugins.
+ Builds plugins will be executed during the build, they should be configured in the <build /> element.
+ Reporting plugins will be executed during the site generation and they should be configured in the <reporting /> element.



### Maven Goals

+ All plugins should have minimal required information: groupId, artifactId and version.
+ Whenever you want to customise the build for a Maven project, this is done by adding or re-configuring plugins.
+ Plugins are artifacts that provide Goals to Maven.
+ A plugin may have one or more Goals where each goal represents a capability of that plugin.



### Maven-compiler-plugin

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.0</version>
            <configuration>
                <target>11</target>
                <source>11</source>
                <release>11</release>
            </configuration>
        </plugin>
    </plugins>
</build>
```



### Logging

**Logback Classic** from MavenRepository.

Why don't need the '<scope>test</scope>'.

```xml
<dependencies>
	<dependency>
    	<groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```



**Simple Example**

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloMaven {

    private final static Logger log = LoggerFactory.getLogger(HelloMaven.class);

    public static void main(String[] args) {
        log.info("Hello Info");
        log.debug("Hello Debug");
    }
}
```



**Configuration**

It could named 'logback.xml' in the resources folder.

```xml
<configuration>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%date [%thread] [%-5level] %logger{40} - %message%n</pattern>
        </encoder>
    </appender>

    <logger name="academy.learnprogramming" level="DEBUG" />

    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
</configuration>
```

