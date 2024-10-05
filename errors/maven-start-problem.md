@TuncerKARAARSLAN-VB ➜ /workspaces/spring-boot-hello-world (main) $ ./mvnw spring-boot:run
bash: ./mvnw: No such file or directory

---

```md
If you encounter the error `bash: ./mvnw: No such file or directory`, it means the `mvnw` (Maven Wrapper) script is missing from your project directory. This script is typically generated when you create a new Spring Boot project using Spring Initializr or another generator.

### Steps to resolve the issue:

1. **Verify the Project Structure**:  
   Ensure you are in the root directory of the Spring Boot project, where the `mvnw` script should be located. Use the `ls` command to list files in the directory:
   ```bash
   ls
   ```

2. **Download a New Project with Maven Wrapper**:  
   If you are starting a new project, make sure to include the Maven wrapper by adding the `-d type=maven-project` flag to your `curl` command:
   ```bash
   curl https://start.spring.io/starter.zip -d dependencies=web -d language=java -d javaVersion=17 -d type=maven-project -o spring-boot-hello-world.zip
   unzip spring-boot-hello-world.zip -d .
   ```

3. **Run the Spring Boot Application**:  
   After downloading the correct project files, navigate to the project directory and run the following:
   ```bash
   ./mvnw spring-boot:run
   ```

If you want to generate the Maven Wrapper manually for an existing project, you can run this command:
   ```bash
   mvn wrapper:wrapper
   ```

This will create the `mvnw` and `mvnw.cmd` files required for running Maven commands.
```