# Created By Ramaprasad # 

This guide provides step-by-step instructions for deploying a Java Hello World application using Maven, Jenkins, Docker, and Kubernetes.

### Table of Contents ### 

Run Maven Clean and Install

Build the Executable JAR

Run the Executable JAR

Install Jenkins

Create Jenkins Pipeline

Build and Push Docker Image

Deploy to Kubernetes

Access the Application

Cleanup

1. Run Maven Clean and Install
Execute the following Maven commands to clean your project and install dependencies:

# mvn clean
# mvn install

2. Build the Executable JAR
Run the Maven package goal to build the executable JAR:


# mvn package
This command will create an executable JAR file in the target directory.

3. Run the Executable JAR
After the build is successful, you can run the generated JAR file using the following command:


# java -jar target/jb-hello-world-maven-0.2.0.jar
Adjust the JAR filename based on the actual filename generated by Maven.

4. Install Jenkins
Update the package list

# sudo apt-get update
Install Java Development Kit (JDK)

# sudo apt-get install -y openjdk-8-jdk
Add the Jenkins repository key and update the package list

# wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
# sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
# sudo apt-get update
Install Jenkins

# sudo apt-get install -y jenkins
Start Jenkins service
# sudo systemctl start jenkins

5. Create Jenkins Pipeline
   
Open the Jenkins dashboard using Username and Password.

Click on "New Item."

Choose "Pipeline" and enter a name.

Define the pipeline script.

Save the pipeline job.

Click "Build Now" to run the pipeline.

6. Build and Push Docker Image
Build Steps:
Navigate to the directory:
# cd /path/to/your/java/application

Build the Docker Image:
# docker build -t java-application:latest .

Run the Docker Container Locally:
# docker run -p 8080:8080 java-application:latest

Push Steps:
Log in to Docker Hub:
# docker login -u gudururamaprasad

Push the Docker Image:
# docker push java-application:latest

7. Deploy to Kubernetes

Step 1: Apply the Deployment YAML

Save the Kubernetes Deployment YAML content in a file, for example, java-hello-world-deployment.yaml.

 Then, apply the deployment to your Kubernetes cluster:
 
# kubectl apply -f java-hello-world-deployment.yaml

Step 2: Verify Deployment
Check the status of the deployment:

# kubectl get deployments
Step 3: Expose the Deployment
If your application is meant to be accessed externally, you need to expose it. Create a Kubernetes Service:


# kubectl expose deployment java-hello-world-app --type=NodePort --port=8080
Step 4: Verify Service

Check the status of the service:
# kubectl get services

Step 5: Access the Application
If you are using a local Kubernetes cluster, use the following command to get the URL:


# minikube service java-hello-world-app
If you are using a cloud-based Kubernetes cluster, access the application using the external IP or domain associated with your service.

Step 6: Cleanup 
If needed, you can delete the deployment and service:

# kubectl delete deployment java-hello-world-app
# kubectl delete service java-hello-world-app
