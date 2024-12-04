# Script to install Jenkins

This script simplifies the installation of Java 17 and Jenkins on Debian-based Linux or macOS systems. It detects the operating system (Debian or macOS) and uses the appropriate package manager (`apt` for Debian, `brew` for macOS) to install the required packages. The script handles prerequisites, adds the Jenkins repository (for Debian), and completes the software installation. By automating these repetitive setup steps, it streamlines the process of configuring an environment for Jenkins.

![1](https://github.com/user-attachments/assets/869af7c8-2be9-46b8-ac6a-6b5ffb673450)

This Bash script automates the installation of Java 17 and Jenkins on Ubuntu, Red Hat, or macOS platforms. The `identify_platform` function detects the OS type using `OSTYPE` and available package managers (`apt`, `yum`, or `brew`). Based on the detected platform, `setup_java` installs OpenJDK 17, and `setup_jenkins` installs Jenkins using the appropriate package manager and keys. Both functions handle platform-specific commands to ensure compatibility. The script exits if an unsupported platform is detected. The `execute_tasks` function orchestrates the process, running platform detection first and then sequentially setting up Java and Jenkins. Finally, it provides guidance to access Jenkins via a browser.

# Setup Master-slave architecture
Setting up a node for a master-slave architecture by utilizing the private key, username, and host details from a remote system, and it is capable of executing 5 tasks at a time

![2](https://github.com/user-attachments/assets/7655d6e1-9d87-4467-b9f5-bf5b3da62d23)

![2 1](https://github.com/user-attachments/assets/eaceac1a-ca76-4dd4-969b-03eeceb926d9)

This was done to run upto 5 different types of task as per their demand

# Setup Role based authorization
Create a item role named project_show with pattern of "project.*" and from the job section give it permission of build, configure, read and workspace.

![3](https://github.com/user-attachments/assets/639826f8-4a95-4fb7-945c-7a75dc23a2a7)

Create a Global roles named project and give it permisson of project_view. Add user project in item roles, give it the permission of project_view.

![3 1](https://github.com/user-attachments/assets/e2be156a-a56c-42d0-8fbf-1b9d13c7b41c)

Login from the project user(I have given my user name control)

![3 2](https://github.com/user-attachments/assets/63a258bb-e4f9-4e7b-930b-263bdd8dfe4e)

Now we will observe the project with same patterns

![Screenshot from 2024-12-05 00-21-31](https://github.com/user-attachments/assets/f5b067e2-9e70-43b2-bdf7-30f7f721e873)

# Create a pipeline to execute a shell script, on git, on scripting task, Monitor disk utlization and send mail if > 80%, Process Management, take inputs, check for errors, cleanup, backup, logging.

The scripts required to execute the pipeline, including JenkinsFile, bullet.sh, script1.sh, and script2.sh, are available on GitHub.

![5](https://github.com/user-attachments/assets/134af8e8-a160-4bd1-bf75-1c8339ecb224)

The Jenkins pipeline performs automation in three stages: Git Checkout (cloning the repository), Disk Usage Check (executing script1.sh), and Process Management (executing bullet.sh). It is configured to run hourly and sends failure notifications via email, providing job details and a link to the console output for troubleshooting.

![5 1](https://github.com/user-attachments/assets/cb96ce5c-e335-42c1-b332-247afde2579e)

This Bash script monitors system resources by identifying processes consuming the most CPU and memory. It uses ps aux to sort and display the top resource-intensive processes. Additionally, it detects zombie processes (in the "Z" state) with the help of awk, aiding in efficient process management and troubleshooting.

![5 3](https://github.com/user-attachments/assets/049f6afc-aebd-4e70-a98c-9331b15362c0)

This Bash script monitors the root directory's disk usage percentage. If usage exceeds 80%, it displays a warning message and exits with an error code. Otherwise, it confirms that disk usage is within safe limits. This proactive method helps administrators manage potential disk space issues effectively.

![5 2](https://github.com/user-attachments/assets/169e521d-8a54-4751-a13c-3e1aff0d1b03)

This Bash script automates backups with optional compression. It accepts source and destination directories, validates their existence, and creates the destination if necessary. Backups are uniquely timestamped, compressed when the -c flag is used, or simply copied. Operations are logged for tracking, and backups older than 7 days are removed to conserve space, ensuring efficient and dependable data protection.

![5 4](https://github.com/user-attachments/assets/6149836b-7278-450b-acd2-e055e5c90387)

![5 5](https://github.com/user-attachments/assets/45478f23-8599-4cb9-abd5-957b3db00df0)

# Build Java app and trigger pipeline

This ensures the installation of Java 17 with the specified version.

![4](https://github.com/user-attachments/assets/fa6f4cd6-255e-47ce-93c5-6a861c73b84e)

This ensures the installation of Maven 3.9.9

![4 1](https://github.com/user-attachments/assets/b5a4a5c7-9e95-45c9-9b38-d1e9a652b08c)

This Jenkins pipeline automates the build, test, and deploy workflow for a Java project. It pulls code from a Git repository, builds it with Maven (skipping tests during packaging), and runs tests with results published using JUnit. The "Deliver" stage executes a deployment script (deliver.sh). The pipeline supports branch selection via parameters and triggers builds on GitHub pushes. Configured to use Maven 3.9.9 and Java 17, it enforces a 10-minute timeout for execution. Post-build steps include archiving artifacts, cleaning the workspace, and logging the pipeline status (success or failure). This setup ensures streamlined, automated, and reliable builds with integrated testing and deployment.

![4 2](https://github.com/user-attachments/assets/25144d28-95fa-48c1-a018-1de3b7d42146)

The Jenkins pipeline now includes the GitHub repository and allows branch selection via a parameter.

![4 3](https://github.com/user-attachments/assets/f0d554d6-13f1-4a04-8de7-8bbfedd822c2)

In the pipeline section, set the definition to Pipeline script from SCM, specifying the Git repository and using */main as the branch specifier.

![4 4](https://github.com/user-attachments/assets/6edc49ba-94c1-410a-a1b4-449e412f9da4)

The script path is specified as example-app-pipeline/Jenkinsfile, where the pipeline script is executed from.

![4 5](https://github.com/user-attachments/assets/f411fc03-7e31-4293-8c1c-79a6a6198af6)
