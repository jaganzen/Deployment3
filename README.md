<p align="center">
<img src="https://github.com/kura-labs-org/kuralabs_deployment_1/blob/main/Kuralogo.png">
</p>
<h1 align="center">C4_deployment-3<h1> 

Certainly! Here's a markdown-formatted `README.md` for your project based on the information you've provided:

---

# Automating Pipeline with GitHub and Elastic Beanstalk

This project aims to automate the process of creating a pipeline using GitHub and AWS Elastic Beanstalk. We also incorporated a webhook to trigger our pipeline whenever changes are made to our GitHub repository. This is made possible by directly linking Jenkins to our GitHub repository.

## Issues Faced

During deployment, we encountered issues with conflicting dependencies and packages. The conflicts arose mainly due to the order in which we executed certain steps.

## Deployment Instructions

### 1. Setup GitHub Repository

Drag and drop your project files directly from your Macbook into your GitHub repository.

### 2. Configure Personal Access Token on GitHub

- Navigate to your GitHub settings.
- Create a new Personal Access Token.
- Grant permissions for `hook` and `repo:hook`.

### 3. Jenkins Server Setup

You can either set up Jenkins manually or use the automation script provided below.

#### Using the Automation Script:

```bash
#!/bin/bash
# Import Jenkins Key
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
sleep 3


# Add Jenkins to the sources.list
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sleep 3

# Update the package list
sudo apt-get update
sleep 3

# Install fontconfig and openjdk-17-jre
sudo apt-get install fontconfig openjdk-17-jre
sleep 3

# Install Jenkins
sudo apt-get install jenkins
sleep 3

echo "All of your packages for Jenkins have been downloaded!"
```

#### Additional Packages:

Before proceeding, install the following packages:

- `Python3.10-venv`
- `unzip`

> **Note**: These packages are installed first to avoid potential conflicts with the `pip` package.

### 4. Create a Multibranch Pipeline

After setting up Jenkins, create a multibranch pipeline and initiate the build for your application.

### 5. AWS Setup

Follow the provided guides to set up AWS CLI and AWS EB CLI:

- [How to Install AWS CLI](https://scribehow.com/shared/How_to_Install_AWS_CLI__1MnhqmpcRxupkx_F-EcreQ)
- [How to install AWS EB CLI](https://scribehow.com/shared/How_to_install_AWS_EB_CLI__J6eBRB9FQl2fGenfUVemlA)

### 6. Deployment Stage

Upon successful build and test, you should see the following stage:

```
Application Deployed Successfully
```

### 7. Webhook Configuration

To configure a webhook for Jenkins deployment using GitHub, follow the guide:

- [Setting up a GitHub webhook for Jenkins deployment](https://scribehow.com/shared/Setting_up_a_GitHub_webhook_for_Jenkins_deployment__OCRQGNvARfWF4clyeFcsGQ)

---

## Additional Resources

If you need additional setup details for IAM Profiles, refer to the instructions provided in "Deployment 1".

---

This `README.md` file is structured to provide a clear understanding of the project and its setup process. Adjustments can be made based on project specifics or any additional details you'd like to add.
