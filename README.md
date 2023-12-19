# Devops-CI-CD-Pipelines-on-AWS

## GitHub Integration with Jenkins

### 1. Installing Git on Jenkins:

Log into the Jenkins server.

Install Git using the package manager (e.g., yum install git).

### 2. Installing GitHub Plugin:

Access the Jenkins dashboard.

Navigate to "Manage Jenkins" > "Manage Plugins" > "Available."

Search and install the GitHub plugin.

### 3. Configuring Git on Jenkins:

Go to "Manage Jenkins" > "Global Tool Configuration."

Set up Git, specifying its name and executable path.

### 4. Creating a Jenkins Job to Pull Code from GitHub:

Create a new job (e.g., "Pull Code from GitHub").

Choose the "Git" option under source code management.

Provide the GitHub repository URL.

Specify credentials if needed.

Save the job.

### 5. Building the GitHub Integration Job:

Execute the job to pull code from the GitHub repository.

## Maven Integration with Jenkins

### 1. Installing Maven on Jenkins:

Download Maven binary tar.gz.

Extract the tar.gz file to a directory like /opt.

Update the Bash profile with Maven and Java environment variables.

### 2. Installing Maven Plugin:

Access the Jenkins dashboard.

Navigate to "Manage Jenkins" > "Manage Plugins" > "Available."

Search and install the Maven Integration plugin.

### 3. Configuring Maven on Jenkins:

Go to "Manage Jenkins" > "Global Tool Configuration."

Add Maven, specifying its name and home directory.

### 4. Creating a Maven Project Build Job:

Create a new Maven project job (e.g., "FirstMavenProject").

Choose Maven project type.

Specify the GitHub repository URL.

Set the build goals (e.g., clean install).

Save the job configuration.

### 5. Building the Maven Project:

Execute the Maven project job.

View the console output to check for a successful build and artifact creation.

## Integrating Tomcat with Jenkins

###  a. Install "Deploy to Container" Plugin:

Install the "Deploy to Container" plugin through the Jenkins dashboard.

Manage Jenkins > Manage Plugins > Available > Search for "Deploy to Container" > Install without restart.

### b. Configure Tomcat Credentials:

Go to Manage Jenkins > Manage Credentials.

Add new credentials for Tomcat, specifically for deploying, using the "deployer" user with the "manager-script" role.

### 2. Creating Jenkins Job for Build and Deploy

a. Create a New Jenkins Job:

Go to Jenkins dashboard.

Create a new Jenkins job (e.g., BuildAndDeployJob) as a Maven project.

Set up the Git repository URL for the source code.

Configure the job to pull code from the master branch.

b. Configure Maven Goals:

Set Maven goals to "clean install" for building the project.

c. Configure Post-Build Actions:

Enable "Deploy to container" option in post-build actions.

Specify the location of the WAR file (e.g., **/*.war).

Add container details (Tomcat 8.x) and use the credentials configured earlier.

### 3. Automating Jenkins Job Execution

a. Set up Build Triggers:

Go to the job configuration.

Under Build Triggers, choose "Poll SCM" and set a schedule using Cron syntax.

Alternatively, use "Build periodically" if you want the job to run at specific times, regardless of code changes.

### 4. Code Changes and Automation

a. Clone Code to Local Workstation:

Clone the GitHub repository onto the local workstation.

b. Update and Commit Code:

Make changes to the source code (e.g., update index.jsp for better formatting).

Commit changes to the local repository.

Push changes to the GitHub repository.

c. Automated Build and Deployment:

Jenkins, with polling enabled, detects changes in the GitHub repository.

Initiates the build job automatically without manual intervention.

d. Observing Build Results:

Monitor the Jenkins job execution in real-time.

## Setting Up Docker Host

### 1. Integration with Jenkins:

Docker host integration with Jenkins is established.

### 2. New Jenkins Job:

A new Jenkins job is created for code integration and deployment.

Configuration involves pulling code from GitHub, building with Maven, and copying artifacts to the Docker host.
### 3. Publish Over SSH Plugin:

Use of the "Publish Over SSH" Jenkins plugin for artifact transfer to the Docker host.

### 4. Artifact Location:

Artifacts (WAR files) are copied to the specified location on the Docker host.

## Creating a New Jenkins Job for Code Deployment

### 1. Open Jenkins:

Create a new Jenkins job named "BuildAndDeployOnContainer."

Copy configuration from an existing job named "BuildAndDeployJob."

Configure the job to copy artifacts to Docker host using the Publish Over SSH plugin.

Execute the Jenkins job to build the code and transfer artifacts to the Docker host.

### 2. Modifying Jenkins Job Configuration for Docker Commands:

Edit the existing Jenkins job to include Docker build and Docker run commands.

Add commands to navigate to /opt/docker, build the Docker image, and create a Docker container.

Execute the Jenkins job, triggering the automated process.

### 3. Handling Docker Container Naming Conflicts:

Include commands for stopping and removing containers before creating a new one.

Execute the Jenkins job to create Docker containers without conflicts.

### 4. Making Changes to the Code and Automated Deployment:

Demonstrate making changes to the code (e.g., adding a new field in index.jsp for name).

Commit changes using Git commands.

Example: git commit -am "updated index.jsp".

Observe the Jenkins job automatically triggered by the code changes.

Verify that the updated code is successfully deployed.

## Setting Up Ansible

### 1. Install Ansible:

Install Ansible on your Ansible server using the appropriate package manager.

### 2. Create an Ansible Inventory:

Define an Ansible inventory file (hosts) specifying the target Docker host.

### 3. Ansible Configuration:

Configure Ansible settings in the ansible.cfg file, if necessary.

### 4. Create Docker Image Playbook (Docker_image_playbook.yml):

Develop an Ansible playbook to build a Docker image.

Utilize the docker_image Ansible module for this task.

Include tasks to stop existing containers and remove existing containers and images.

### 5. Run Docker Image Playbook:

Execute the Docker image playbook on the Ansible server to build the Docker image.

Use Jenkins to trigger this playbook.

### 6. Log in to Docker Hub:

Use the docker login command in Ansible to log in to Docker Hub from the Ansible server.

### 7. Push Docker Image to Docker Hub:

Create a tag for the Docker image using docker tag.

Use docker push to push the Docker image to Docker Hub.

### 8. Create Deployment Ansible Playbook (deploy_playbook.yml):

Develop an Ansible playbook for deployment.

Include tasks to stop existing containers, remove containers/images, and deploy a new container.

### 9. Consolidate Playbooks into One (ci_cd_playbook.yml):

Combine the Docker image playbook and deployment playbook into a single Ansible playbook (ci_cd_playbook.yml).

Adjust paths, variables, and tasks accordingly.

### 10. Jenkins Configuration:

Add a build step in Jenkins to execute the consolidated playbook.

## Setting Up Kubernetes

### 1. Why Setting Up Kubernetes:

Kubernetes is a powerful tool for managing containerized applications.

It provides orchestration, scaling, and management capabilities for containers.

### 2. Bootstrap Server Setup:

A Bootstrap server is set up within the Kubernetes environment.

Ansible is integrated with the Bootstrap server for automation.

### 3. Ansible Playbooks for Kubernetes:

Ansible playbooks are created to define the deployment and service files for Kubernetes.

These playbooks automate the process of deploying applications to Kubernetes.

### 4. Jenkins Integration:

Jenkins, a CI/CD tool, is introduced to automate the deployment process.

A Jenkins job named "Deploy_On_Kubernetes" is created to execute Ansible playbooks.

### 5. Execution of Ansible Playbooks through Jenkins:

Ansible playbooks are executed automatically through Jenkins.

Playbooks are configured to run as the root user for successful execution.

### 6. CI and CD Jobs:

CI (Continuous Integration) and CD (Continuous Deployment) jobs are created in Jenkins.

CI job builds the code, while the CD job deploys the application.

### 7. Integration of CI and CD Jobs:

The CI job triggers the CD job upon successful completion.

Any changes to the source code initiate the CI/CD pipeline.

### 8. Source Code Update:

Source code changes are made (e.g., modifying an index.jsp file).

Changes are committed to the GitHub repository to trigger the CI/CD pipeline.

Check build status (success/failure) and console output for details.
