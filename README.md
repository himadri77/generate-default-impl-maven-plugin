generate-default-impl-maven-plugin
==================================
This plugin is intended to generate an empty implementation of an arbitrary Java interface.
Let's look an example. Provided we have an interface like:

```java
public interface TestInterface
{
    char getChar(String param);
    float getFloat();
    int getInt(List<String> param);
    boolean isBoolean();
    String getName(String firstName);
    void doSomething();
}
```

This tool generates the following code:

```java
public class TestInterfaceDefaultImpl implements com.company.TestInterface {
     @Override public char getChar(java.lang.String p1) {return 0;}
     @Override public float getFloat() {return 0;}
     @Override public int getInt(java.util.List p1) {return 0;}
     @Override public boolean isBoolean() {return false;}
     @Override public java.lang.String getName(java.lang.String p1) {return null;}
     @Override public void doSomething() {}
}
```

This means that for every primitive type it returns a 0 or false, and for every object ot returns null.
After you activate this plugin in your generate-sources maven phase, you can override the generated class.

You can activate the plugin with the following maven snippet:
```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.github.himadri77</groupId>
            <artifactId>generate-default-impl-plugin</artifactId>
            <version>1.3</version>
            <configuration>
                <interfaces>
                    <interface>com.company.TestInterface</interface>
                    <interface>com.company.MyInterface2</interface>
                </interfaces>
                <targetPackage>com.company.generatedstuff</targetPackage>
            </configuration>
            <executions>
                <execution>
                    <goals>
                        <goal>generate-default-impl</goal>
                    </goals>                        
                </execution>
            </executions> 
            <dependencies>                    
                <dependency>
                    <groupId>${project.groupId}</groupId>
                    <artifactId>${project.artifactId}</artifactId>
                    <version>${project.version}</version>
                </dependency>                    
            </dependencies>
        </plugin>
    </plugins>
</build>    
```

Other optional configuration parameters:
```xml
 <configuration>
     <!-- The generated class name will be the interface name + classNamePostfix parameter -->
     <!-- Default: DefaultImpl -->    
     <classNamePostfix>DefaultImpl</classNamePostfix> 
     
     <!-- Where to put the generated java files -->
     <!-- Default: ${project.build.directory}/generated-sources/java -->    
     <outputDirectory>${project.build.directory}/generated-sources/java</outputDirectory>     
 </configuration>             
```
