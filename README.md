<p align="center">
<img src="https://github.com/kura-labs-org/kuralabs_deployment_1/blob/main/Kuralogo.png">
</p>
<h1 align="center">C4_deployment-3<h1> 

---

# Automating Pipeline with GitHub and Elastic Beanstalk

The goal of this project is to automate the process of creating a pipeline using GitHub and AWS Elastic Beanstalk. I had incorporated a webhook to trigger our pipeline whenever changes are made to our GitHub repository. This is made possible by directly linking Jenkins to our GitHub repository.

## Issues Faced

During deployment, we encountered issues with conflicting dependencies and packages. The conflicts arose mainly due to the order in which we executed certain steps.
Thanks to one of my colleagues, and failing at deploying the project at several attempts, we had to make sure that we downloaded our pip packages AFTER we created our Multibranch Pipeline. 

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

After setting up Jenkins, create a multibranch pipeline and initiate the build for your application. And add your Github login credentials with the personal access token that was made.
![Jenkins1](https://github.com/jaganzen/Deployment3/assets/101806502/3322b810-03af-43d2-b93a-90f71d0ea29d)

![Jenkins 2](https://github.com/jaganzen/Deployment3/assets/101806502/1373f29b-cf0b-402c-8712-a433085afa27)

![Screenshot 2023-09-15 at 11 00 30 PM](https://github.com/jaganzen/Deployment3/assets/101806502/ec89bc44-84f1-41c1-9c26-ff535406d395)

### 5. AWS Setup

Before proceeding, install the following packages:

- `sudo apt install python-pip`
- `sudo apt install python3-pip`

Follow the provided guides to set up AWS CLI and AWS EB CLI:

- [How to Install AWS CLI](https://scribehow.com/shared/How_to_Install_AWS_CLI__1MnhqmpcRxupkx_F-EcreQ)
- [How to install AWS EB CLI](https://scribehow.com/shared/How_to_install_AWS_EB_CLI__J6eBRB9FQl2fGenfUVemlA)

### 6. Deployment Stage

Upon successful build and test, you should see this: 
![Build Success](https://github.com/jaganzen/Deployment3/assets/101806502/156b98a9-593e-4149-8c11-8cd8d277e9c1)

![Build Success 2](https://github.com/jaganzen/Deployment3/assets/101806502/8d577bcb-7a0a-485f-856e-d641a2ab3b5e)

![Screenshot 2023-09-16 at 1 19 19 AM](https://github.com/jaganzen/Deployment3/assets/101806502/a99f84b2-9ebc-4764-8544-77696887c8b8)


### 7. Webhook Configuration

To configure a webhook for Jenkins deployment using GitHub, follow the guide:

- [Setting up a GitHub webhook for Jenkins deployment](https://scribehow.com/shared/Setting_up_a_GitHub_webhook_for_Jenkins_deployment__OCRQGNvARfWF4clyeFcsGQ)

What our deployment looked like before we configured the webhook:
<img width="1361" alt="Before" src="https://github.com/jaganzen/Deployment3/assets/101806502/61da6623-d68f-4f4e-8feb-ef9a8e9d16fb">

What our deployment looks like after we configure the webhook (in the red box):
<img width="1680" alt="Deployment 3 Complete" src="https://github.com/jaganzen/Deployment3/assets/101806502/2105fbb3-216d-4d7a-badb-658a02f2f462">


---

## Additional Resources

If you need additional setup details for IAM Profiles, refer to the instructions provided in "Deployment 1".

---

![Deployment 3 drawio](https://github.com/jaganzen/Deployment3/assets/101806502/4265030f-e46d-45f1-a29b-6f5b5133470f)


