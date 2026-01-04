## Creating a job (freestyle)

1. You need to install JAVA to run jenkins so it can compile, bundle and run the tests and create builds to run the application.
2. **Global configuration tool:** You will need to install various versions of Java, you can download them from oracle or https://adoptium.net/temurin/releases
	a. Jenkins uses Java to start and run jobs to compile and run tests and other tasks that agents perform.
	b. **Settings -> Tools:** You need to add the name of the Java Version and its path. The path needs to be where Java version is installed, example:
```
Enter the path for **JAVA_HOME**.
   
Example:
	JAVA_HOME: C:\Program Files\Java\jdk-23
```

#### Credentials and Creating SSH key for Github

For credentials setup you will need to setup the SSH key first and then add it into the Jenkins Credentials section.
#### Credentials

1. To maximize security, credentials configured in Jenkins are stored in an encrypted form on the controller Jenkins controller (encrypted by the Jenkins controller ID) and are only handled in Pipeline projects via their credential IDs.
2. This minimizes the chances of exposing the actual credentials themselves to Jenkins users and hinders the ability to copy functional credentials from one Jenkins controller to another.
3. **Configuring credentials of kind SSH:** https://www.jenkins.io/doc/book/using/using-credentials/#configuring-credentials
#### SSH Hash keys for github

1. **Create SSH Keys:** https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
2. **How to add them on github:** You need to add the public key on github and use the Private key at your end, or in Jenkins case, you need to add the *complete private key including the begin + end line in the field of credentials on jenkins.* LINK: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account


demo-app-java-project

hashkey: C:\Program Files\Eclipse Adoptium\jdk-11.0.29.7-hotspot

#### 8.1 Steps running a free-style Maven Job

1. How Maven works (simple)
	a. Project has a `pom.xml`
    b. `pom.xml` defines:
    - Dependencies
    - Plugins
    - Build steps
	c. Maven follows a **fixed lifecycle**

```
clean → compile → test → verify → package → install
```
2. What is ***“Invoke top-level Maven targets”*** in Jenkins
	a.  Jenkins needs a **standard way to run Maven**
	b. This option tells Jenkins:
	c. “Run Maven using the lifecycle defined in pom.xml”

It is **not a template**, it’s the **correct Maven execution method**.

3. What `clean verify site` mean:
- `clean` → remove old builds
- `verify` → run tests & checks
- `site` → generate reports (JaCoCo, PMD, SpotBugs)

3. ***Why we used Github?*** Cloned an example project
	a. GitHub stores the **source code + pom.xml**
	b. Jenkins: `pulls code → runs Maven → generates reports`
	c. Maven **does not run code from GitHub directly** — Jenkins does.
4. **Difference between MAVEN and NODEJS**
	a. MAVEN is a Build Tool
	b. NODE JS is a runtime engine
	c. Java runs on the **JVM**, Maven just prepares it.

### 8.2 SUMMARY OF THE FREESTYLE JOB

1. A CI/CD pipeline job using Jenkins and GitHub to monitor builds and generate reports
2. **Maven** is a build automation tool for Java that compiles code, runs tests, manages dependencies, and generates quality reports.
3. Set up GitHub SSH credentials in Jenkins
4. Installed JDK 11 and Maven via Global Tool Configuration
5. Created a Freestyle Jenkins job 
6. Configured SCM polling 
7. Built the project using Maven goals (clean verify site)
8. Integrated code quality & coverage tools (JaCoCo, PMD, SpotBugs)
9. Recorded static analysis results using Jenkins plugins