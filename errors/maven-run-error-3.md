./mvnw spring-boot:run
[INFO] Scanning for projects...
[INFO] 
[INFO] ----------------< com.example:spring-boot-hello-world >-----------------
[INFO] Building spring-boot-hello-world 0.0.1-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] >>> spring-boot:2.5.4:run (default-cli) > test-compile @ spring-boot-hello-world >>>
[INFO] 
[INFO] --- resources:3.2.0:resources (default-resources) @ spring-boot-hello-world ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered properties files.
[INFO] Copying 1 resource
[INFO] Copying 0 resource
[INFO] 
[INFO] --- compiler:3.8.1:compile (default-compile) @ spring-boot-hello-world ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- resources:3.2.0:testResources (default-testResources) @ spring-boot-hello-world ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered properties files.
[INFO] skip non existing resourceDirectory /workspaces/spring-boot-hello-world/src/test/resources
[INFO] 
[INFO] --- compiler:3.8.1:testCompile (default-testCompile) @ spring-boot-hello-world ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to /workspaces/spring-boot-hello-world/target/test-classes
[INFO] -------------------------------------------------------------
[ERROR] COMPILATION ERROR : 
[INFO] -------------------------------------------------------------
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[3,29] package org.junit.jupiter.api does not exist
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[4,45] package org.springframework.boot.test.context does not exist
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[6,2] cannot find symbol
  symbol: class SpringBootTest
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[9,10] cannot find symbol
  symbol:   class Test
  location: class com.example.demo.DemoApplicationTests
[INFO] 4 errors 
[INFO] -------------------------------------------------------------
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.276 s
[INFO] Finished at: 2024-10-05T13:20:24Z
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.8.1:testCompile (default-testCompile) on project spring-boot-hello-world: Compilation failure: Compilation failure: 
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[3,29] package org.junit.jupiter.api does not exist
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[4,45] package org.springframework.boot.test.context does not exist
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[6,2] cannot find symbol
[ERROR]   symbol: class SpringBootTest
[ERROR] /workspaces/spring-boot-hello-world/src/test/java/com/example/demo/DemoApplicationTests.java:[9,10] cannot find symbol
[ERROR]   symbol:   class Test
[ERROR]   location: class com.example.demo.DemoApplicationTests
[ERROR] -> [Help 1]
[ERROR] 
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR] 
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoFailureException

---

The error messages you're encountering indicate that the JUnit and Spring Boot testing dependencies are missing from your `pom.xml` file. This results in compilation errors because classes like `SpringBootTest` and `Test` cannot be found.

### Steps to Resolve the Compilation Errors:

1. **Add Testing Dependencies**:
   You need to add the appropriate JUnit and Spring Boot test dependencies to your `pom.xml`. Below is an updated example of how your `pom.xml` might look with the necessary dependencies:

   ```xml
   <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>

       <groupId>com.example</groupId>
       <artifactId>spring-boot-hello-world</artifactId>
       <version>0.0.1-SNAPSHOT</version>
       <name>spring-boot-hello-world</name>
       <description>Demo project for Spring Boot</description>
       <parent>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-parent</artifactId>
           <version>2.5.4</version>
           <relativePath/> <!-- lookup parent from repository -->
       </parent>

       <properties>
           <java.version>17</java.version>
       </properties>

       <dependencies>
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-web</artifactId>
           </dependency>
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-test</artifactId>
               <scope>test</scope>
           </dependency>
       </dependencies>

       <build>
           <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
           </plugins>
       </build>
   </project>
   ```

2. **Ensure the `spring-boot-starter-test` Dependency is Included**:
   In the `<dependencies>` section, ensure that the `spring-boot-starter-test` dependency is included with the `<scope>` set to `test`. This dependency includes JUnit and other testing tools.

3. **Save Changes to `pom.xml`**:
   After adding the necessary dependencies, save the `pom.xml` file and exit your text editor.

4. **Rebuild the Project**:
   Run the following command to rebuild the project and resolve dependencies:
   ```bash
   ./mvnw clean install
   ```

5. **Run the Spring Boot Application Again**:
   After the build is successful, try running your Spring Boot application again:
   ```bash
   ./mvnw spring-boot:run
   ```

Following these steps should resolve the compilation errors and allow you to successfully run your Spring Boot application. If you encounter further issues, make sure that your project structure is correct and that all necessary files are in place.

