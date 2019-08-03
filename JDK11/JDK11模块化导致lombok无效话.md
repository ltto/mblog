# JDK11 module-info.java 模块化 lombok失效问题
``` java
module demo { 
    requires static lombok;   
        //static保证运行时不会出现
} 
```
在这里 [https://projectlombok.org/setup/javac](https://projectlombok.org/setup/javac)得知
需要在编译时加载jar 
```sh
javac -cp lombok.jar -p lombok.jar ...
```
如果在maven项目下 
pom.xml
```xml
<build>
        <plugins>
            <plugin>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <annotationProcessorPaths>
                        <path>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                            <version>${lombok.version}</version>
                        </path>
                    </annotationProcessorPaths>
                    <source>11</source>
                    <target>11</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
```