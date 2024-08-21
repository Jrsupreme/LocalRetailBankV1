# Deploying a Retail Bank Web-Application using the CI/CD Pipeline.

**Retail Bank application fully managed by AWS Elastic Beanstalk**

## **Purpose**

The objective here is to demonstrate the deployment of a Continuous Integration/Continuous Deployment (CI/CD) pipeline using Jenkins, GitHub, and AWS Elastic Beanstalk. Emphasizing the practical application of system design principles, the configuration of Jenkins for automated builds, and the deployment of an application in a cloud environment.

## **Steps Taken**

### **1. Cloning the Repository**

- Cloned the repository from GitHub to my account.
- This is the foundation for the entire CI/CD pipeline, as Jenkins needs access to the repository to automate builds.

### **2. Creating an EC2 Instance**

- Launched an EC2 instance on AWS.
- The EC2 instance serves as the host for the Jenkins server. This is crucial as Jenkins automates the build and deployment processes.

### **3. Installing Jenkins on EC2**

- Installed Jenkins using the following commands:

```jsx
sudo apt update && sudo apt install fontconfig openjdk-17-jre software-properties-common && sudo add-apt-repository ppa:deadsnakes/ppa && sudo apt install python3.7 python3.7-venv
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

**Importance**: Jenkins is the core of the CI/CD pipeline, orchestrating the automated testing, integration, and deployment of the application.

### **4. Logging into Jenkins**

- Logged into Jenkins, entered the initial admin password, installed suggested plugins, and created the first admin user.
- This sets up Jenkins for managing and executing the pipeline.

### **5. Creating a Multi-Branch Pipeline**

- Created a Multi-Branch Pipeline in Jenkins, linked it to the GitHub repository.
- The multi-branch pipeline allows Jenkins to automatically trigger builds when changes are detected in any branch of the repository, enabling continuous integration.

### **6. Configuring GitHub Access**

- Generated a GitHub personal access token and configured Jenkins to access the repository.
- Securely connecting Jenkins to GitHub ensures that Jenkins can pull the latest code and automate the build process.

### **7. Running the Build**

- Validated the GitHub repository in Jenkins and ran the pipeline build.
- The build process checks the code for errors and prepares the application for deployment. It ensures that only code that passes all tests is deployed.

**1. Checkout Stage**

- This screenshot shows the Checkout stage, where Jenkins pulls the latest code from the GitHub repository. This step ensures that the pipeline is working with the most up-to-date version of the codebase. It retrieves the code from the specified branch and prepares it for the subsequent stages.

![CheckoutStage](https://github.com/user-attachments/assets/3c7ea3c0-1977-4688-9dba-0232b53d2a10)

**2. Build Stage**

- In this stage, the code is compiled and any necessary dependencies are installed. The screenshot displays the process of Jenkins executing the build commands as defined in the Jenkinsfile. This step is crucial for verifying that the code compiles without errors and that all required components are in place.

![BuildStage](https://github.com/user-attachments/assets/c5da4389-0e57-479a-96b6-45e56a26e17b)

![BuildStage2](https://github.com/user-attachments/assets/181395c1-1afe-4791-86de-eeb59754b56a)

 **3. Test Stage**

- The Test stage is captured here, where Jenkins runs automated tests on the code. This step ensures that the code behaves as expected and that no bugs or issues have been introduced. The screenshot shows the progress of the tests, with a focus on ensuring that all test cases pass successfully.

![TestStage](https://github.com/user-attachments/assets/72c9fb5e-239a-44ce-94a6-1830821513ab)

**4. Successful Build Completion**

- The final screenshot shows the build marked as successful. All stages have been executed without errors, and the application is ready for deployment. This confirmation indicates that the code has passed all necessary checks and is production-ready.
    
![Sucessful build](https://github.com/user-attachments/assets/863182a2-f243-4396-bde6-dd67e0cc614d)


### **8. Deploying to AWS Elastic Beanstalk**

- Created an IAM role, uploaded the application to AWS Elastic Beanstalk, and deployed it using a Python 3.7 environment.
- Elastic Beanstalk simplifies the deployment process, handling capacity provisioning, load balancing, and health monitoring automatically.

## **Issues/Troubleshooting**

- **Issue**: Jenkins failed to validate the GitHub repository.
    - **Resolution**: Realized the personal access token was not properly copied. Generated a new token and reconfigured Jenkins.


# Infracstructure Diagram

![WL1(R) drawio](https://github.com/user-attachments/assets/b67b955a-6b04-499b-a0a9-5a01766507ee)


# Optimization

### Fully Automating the CI/CD Pipeline

- During this deployment the application had to be manually deployed to Elastic beanstalk, which can cause:
    - **Inefficiency:** Manual deployment processes are time-consuming and prone to human error.
    - **Risk of Errors:** Manual steps can introduce inconsistencies and mistakes, leading to potential downtime or security vulnerabilities.
    - **Delayed Time:** Manual deployments can slow down the release cycle.
    - **Solution:** To eliminate/mitigate human error, a deployment stage should be added and configured within Jenkins to automate the deployment/release stage of the pipeline.
    

### **Benefits of Managed Services**

- **Efficiency**: Managed services like Elastic Beanstalk reduce the overhead of managing infrastructure, allowing teams to focus on development.
- **Scalability**: Easily scale the application up or down based on demand without manual intervention.
- **Security**: AWS handles security patches and updates for the underlying infrastructure.

### **Challenges for a Retail Bank**

- **Data Security**: Retail banks handle sensitive customer data, so using managed services might raise concerns about data privacy and control.
    - **Mitigation**: Robust encryption, and enforce strict access controls.

### **Disadvantages of Elastic Beanstalk**

- **Limited Customization**: While Elastic Beanstalk is convenient, it might not support all customization needs for complex applications.
- **Cost**: Managed services can be more expensive than self-managed infrastructure, particularly for large-scale deployments.

## **Conclusion**

This project provided hands-on experience with setting up a CI/CD pipeline using industry-standard tools. By automating the build and deployment processes, we ensured that the application can be continuously tested and delivered efficiently. The use of managed services like AWS Elastic Beanstalk streamlined the deployment but also highlighted the need for careful consideration of security, compliance, and cost.
