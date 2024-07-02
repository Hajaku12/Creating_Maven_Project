# Maven Installation and Project Setup Guide

This guide provides step-by-step instructions for installing Maven, creating a new Maven project, building the project, and setting up Git for version control.

## Installing Maven

### Prerequisites
- Java installed (version 7 or 8)

### Steps to Install Maven

1. **Download Maven**
   - Go to the official Maven website and download the latest version: [Maven Download](http://maven.apache.org/download.html)

2. **Verify Java Installation**
   - Ensure Java is installed by running the following command:
     ```sh
     java -version
     ```
   - You should see an output similar to:
     ```sh
     java version "1.8.0"
     Java(TM) SE Runtime Environment (build 1.8.0-b132)
     Java HotSpot(TM) 64-Bit Server VM (build 25.0-b70, mixed mode)
     ```

3. **Install Maven**
   - Follow the instructions on the Maven download page: [Maven Installation Guide](http://maven.apache.org/download.html#Installation)

4. **Verify Maven Installation**
   - After installation, run the following command to verify Maven is installed correctly:
     ```sh
     mvn -version
     ```
   - The output should look similar to:
     ```sh
     Apache Maven 3.2.5 (12a6b3acb947671f09b81f49094c53f426d8cea1; 2014-12-14T12:29:23-05:00)
     Maven home: /Users/dnielben/Applications/apache-maven-3.2.5
     Java version: 1.8.0, vendor: Oracle Corporation
     Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0.jdk/Contents/Home/jre
     Default locale: es_ES, platform encoding: UTF-8
     OS name: "mac os x", version: "10.10.1", arch: "x86_64", family: "mac"
     ```

---

## Creating a Project

1. **Open a Shell**
   - Open a terminal or command prompt.

2. **Navigate to Your Projects Directory**
   - Change to the directory where you want to store your projects.

3. **Generate a Maven Project**
   - Run the following command to create a new Maven project:
     ```sh
     mvn archetype:generate -DgroupId=edu.escuelaing.arsw.ASE.app -DartifactId=mi-primera-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
     ```
   - Navigate to the newly created project directory:
     ```sh
     cd mi-primera-app/
     ```

---

## Building the Project

1. **Build the Project**
   - Run the following command to build the project:
     ```sh
     mvn package
     ```
   - The output should look similar to:
     ```sh
     [INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ mi-primera-app ---
     [INFO] Building jar: /Users/dnielben/NetBeansProjects/mi-primera-app/target/mi-primera-app-1.0-SNAPSHOT.jar
     [INFO]
     [INFO] BUILD SUCCESS
     [INFO]
     [INFO] Total time: 17.029 s
     [INFO] Finished at: 2015-01-19T13:51:56-05:00
     [INFO] Final Memory: 16M/59M
     ```

   - Note: `package` is a phase, not a plugin. The command executes all phases up to `package`.

2. **Run the Application**
   - Run the following command to execute the application:
     ```sh
     java -cp target/mi-primera-app-1.0-SNAPSHOT.jar edu.escuelaing.arsw.ASE.app.App
     ```

3. **Chaining Phases and Plugin Goals**
   - Clean, copy dependencies, and package the project with:
     ```sh
     mvn clean dependency:copy-dependencies package
     ```

---

## Generating Project Documentation

1. **Generate the Site**
   - Run the following command to generate the site documentation:
     ```sh
     mvn site
     ```

2. **Add Javadoc Plugin for Documentation**
   - Add the Javadoc plugin to the `reporting` section of the `pom.xml`:
     ```xml
     <project>
       ...
       <reporting>
         <plugins>
           <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-javadoc-plugin</artifactId>
             <version>2.10.1</version>
             <configuration>
               ...
             </configuration>
           </plugin>
         </plugins>
       </reporting>
       ...
     </project>
     ```

   - To generate Javadoc as an independent element, add the plugin in the `build` section of the `pom.xml`:
     ```xml
     <project>
       ...
       <build>
         <plugins>
           <plugin>
             <groupId>org.apache.maven.plugins</groupId>
             <artifactId>maven-javadoc-plugin</artifactId>
             <version>2.10.1</version>
             <configuration>
               ...
             </configuration>
           </plugin>
         </plugins>
       </build>
       ...
     </project>
     ```

3. **Generate Javadoc Commands**
   - Use the following commands to generate Javadocs:
     ```sh
     mvn javadoc:javadoc
     mvn javadoc:jar
     mvn javadoc:aggregate
     mvn javadoc:aggregate-jar
     mvn javadoc:test-javadoc
     mvn javadoc:test-jar
     mvn javadoc:test-aggregate
     mvn javadoc:test-aggregate-jar
     ```

---

## Setting Up Git

### Install Git
- Follow the instructions on the Git website: [Git Installation Guide](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

### Verify Git Installation
- Run the following command to verify Git is installed:
  ```sh
  git --version
  ```
- The output should look similar to:
  ```sh
  git version 2.2.1
  ```

### Configure Git Identity and Default Editor
- Set your name and email:
  ```sh
  git config --global user.name "John Doe"
  git config --global user.email johndoe@example.com
  git config --global core.editor emacs
  ```

- Review your configuration:
  ```sh
  git config --list
  ```
- You should see output similar to:
  ```sh
  user.name=Daniel Benavides
  user.email=dnielben@gmail.com
  core.editor=emacs
  ```

### Create a Git Repository
- In your project directory, initialize a Git repository:
  ```sh
  git init
  ```

### Commit Changes to Git
- To create a new version and commit the changes, run:
  ```sh
  git commit -m 'Primera versión del proyecto'
  ```

### List Remote Repositories
- To list remote repositories you have worked with, run:
  ```sh
  git remote
  ```

### Push Changes to Remote Repository
- Push the latest version of your project to the remote repository:
  ```sh
  git push -u origin master
  ```

### Add More Files to Your Git Project and Remote Repository
- It is recommended to create a README, LICENSE, and .gitignore file:
  ```sh
  echo 'Mi primer proyecto' > README.txt
  echo 'TODO: Copiar el texto de la licencia http://www.gnu.org/licenses/gpl.html' > LICENSE.txt
  echo '# TODO: Copiar los contenidos de https://github.com/github/gitignore/blob/master/Java.gitignore' > .gitignore
  ```

- Add the files to the repository:
  ```sh
  git add *.txt
  git add .gitignore
  ```

