# Installation and Configuration Guide pipeline Jenkins automatically trigger

## Install Jenkins

```bash
wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo

rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

yum upgrade

yum install fontconfig java-17-openjdk

yum install jenkins

systemctl daemon-reload

sudo systemctl start jenkins

sudo systemctl enable jenkins

Access Jenkins at: http://<your_server_IP>:8080
```
## Install Git
```bash
yum install git
```
## Setting Up a GitHub Repository 

1. **Create a New GitHub Repository or Select an Existing One**
   - If you're creating a new repository, you can do so by clicking on the '+' icon on the top right of your GitHub profile, then select 'New repository'.
   - If you're using an existing repository, navigate to that repository on GitHub.

2. **Initialize the Repository with a README.md**
   - If you're creating a new repository, you can initialize it with a README.md file by checking the box labeled 'Initialize this repository with a README' during the creation process.
   - If you're using an existing repository, you can add a README.md file by clicking on 'Add a README' on the main page of your repository.

3. **Ensure the Repository Contains at Least Two Branches: 'develop' for Ongoing Development and 'master' (or 'main') for Stable Releases**
   - You can create new branches in your repository by clicking on the 'Branch: master' button (or 'Branch: main' depending on your default branch) on the main page of your repository, then typing the name of the new branch ('develop') and hitting Enter.

## Add a Jenkinsfile 

Add Jenkinsfile to develop branch

```bash
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}

```


## Jenkins Configuration

Install necessary plugins in Jenkins, such as Git and Pipeline. Configure Jenkins to connect to GitHub:

1.Go to “Manage Jenkins” > “Manage Plugins” > “Available” and install “GitHub Integration Plugin”.

![image](https://github.com/AbdElrahmanSaaad/Jenkins/assets/60901149/2475a73e-b75b-4488-9704-15a39a0b1107)

2.Set up credentials in Jenkins for GitHub (username and token).
Create a new pipeline job named “GitHub Pipeline”. In the pipeline configuration, select “Pipeline script from SCM” and choose “Git” as the SCM. Enter the repository URL and credentials. Specify the branch to build (e.g., */develop).

![image](https://github.com/AbdElrahmanSaaad/Jenkins/assets/60901149/b72e7c87-db84-4198-bfe5-12154a601c11)
![image](https://github.com/AbdElrahmanSaaad/Jenkins/assets/60901149/38535b94-9de7-4aaa-a112-5b5d557bd8b6)


3.Scroll down to the “Build Triggers” section.

4.Check the box next to “Poll SCM”.

5.In the “Schedule” field, enter the polling schedule using cron syntax. For example, 
to poll every 5 minutes, you can use H/5 * * * *.

![image](https://github.com/AbdElrahmanSaaad/Jenkins/assets/60901149/b60b5560-9c37-499a-b0e6-46db78e8dd45)

##Testing
Make a commit to your GitHub repository. Jenkins will periodically poll the repository according to the schedule you specified. When Jenkins detects changes in the repository during a polling interval, it will trigger the associated job to run a build.

## Conclusion

After setting up the Jenkins pipeline with GitHub integration and configuring the Jenkins job to poll SCM, you should verify that Jenkins automatically triggers a build when changes are pushed to the GitHub repository. This process should follow the steps defined in the Jenkinsfile.

During the build process, Jenkins will execute the 'Build', 'Test', and 'Deploy' stages as defined in the Jenkinsfile. You should check the output in Jenkins to ensure these stages are executed successfully. If any errors occur, they will be displayed in the Jenkins console output, allowing you to troubleshoot and resolve them.

By successfully setting up this pipeline, you have automated the process of building, testing, and deploying your application. This not only improves efficiency but also ensures consistent quality and faster delivery of features.

![image](https://github.com/AbdElrahmanSaaad/Jenkins/assets/60901149/4c74364a-1c35-4b48-9586-2a05057173e4)

![image](https://github.com/AbdElrahmanSaaad/Jenkins/assets/60901149/56d65d38-16f8-41b9-9e70-d4c4dec76a93)

![image](https://github.com/AbdElrahmanSaaad/Jenkins/assets/60901149/2c57b1e6-ec27-424c-9de5-ef1e1976b37f)
