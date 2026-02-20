![cover-v5-optimized](https://github.com/langgenius/dify/assets/13230914/f9e19af5-61ba-4119-b926-d10c4c06ebab)

<p align="center">
  📌 <a href="https://dify.ai/blog/introducing-dify-workflow-file-upload-a-demo-on-ai-podcast">Introducing Dify Workflow File Upload: Recreate Google NotebookLM Podcast</a>
</p>

<p align="center">
  <a href="https://cloud.dify.ai">Dify Cloud</a> ·
  <a href="https://docs.dify.ai/getting-started/install-self-hosted">Self-hosting</a> ·
  <a href="https://docs.dify.ai">Documentation</a> ·
  <a href="https://udify.app/chat/22L1zSxg6yW1cWQg">Enterprise inquiry</a>
</p>

<p align="center">
  <a href="./README.md"><img alt="README in English" src="https://img.shields.io/badge/English-d9d9d9"></a>
  <a href="./README_CN.md"><img alt="简体中文版自述文件" src="https://img.shields.io/badge/简体中文-d9d9d9"></a>
  <a href="./README_JA.md"><img alt="日本語のREADME" src="https://img.shields.io/badge/日本語-d9d9d9"></a>
  <a href="./README_ES.md"><img alt="README en Español" src="https://img.shields.io/badge/Español-d9d9d9"></a>
  <a href="./README_FR.md"><img alt="README en Français" src="https://img.shields.io/badge/Français-d9d9d9"></a>
  <a href="./README_KL.md"><img alt="README tlhIngan Hol" src="https://img.shields.io/badge/Klingon-d9d9d9"></a>
  <a href="./README_KR.md"><img alt="README in Korean" src="https://img.shields.io/badge/한국어-d9d9d9"></a>
  <a href="./README_AR.md"><img alt="README بالعربية" src="https://img.shields.io/badge/العربية-d9d9d9"></a>
  <a href="./README_TR.md"><img alt="Türkçe README" src="https://img.shields.io/badge/Türkçe-d9d9d9"></a>
  <a href="./README_VI.md"><img alt="README Tiếng Việt" src="https://img.shields.io/badge/Ti%E1%BA%BFng%20Vi%E1%BB%87t-d9d9d9"></a>
</p>


Dify is an open-source LLM app development platform. Its intuitive interface combines agentic AI workflow, RAG pipeline, agent capabilities, model management, observability features and more, letting you quickly go from prototype to production. 

## Quick start
> Before installing Dify, make sure your machine meets the following minimum system requirements:
> 
>- CPU >= 2 Core
>- RAM >= 4 GiB


## Key features
**1. Workflow**: 
  Build and test powerful AI workflows on a visual canvas, leveraging all the following features and beyond.


  https://github.com/langgenius/dify/assets/13230914/356df23e-1604-483d-80a6-9517ece318aa



**2. Comprehensive model support**: 
  Seamless integration with hundreds of proprietary / open-source LLMs from dozens of inference providers and self-hosted solutions, covering GPT, Mistral, Llama3, and any OpenAI API-compatible models. A full list of supported model providers can be found [here](https://docs.dify.ai/getting-started/readme/model-providers).

![providers-v5](https://github.com/langgenius/dify/assets/13230914/5a17bdbe-097a-4100-8363-40255b70f6e3)


**3. Prompt IDE**: 
  Intuitive interface for crafting prompts, comparing model performance, and adding additional features such as text-to-speech to a chat-based app. 

**4. RAG Pipeline**: 
  Extensive RAG capabilities that cover everything from document ingestion to retrieval, with out-of-box support for text extraction from PDFs, PPTs, and other common document formats.

**5. Agent capabilities**: 
  You can define agents based on LLM Function Calling or ReAct, and add pre-built or custom tools for the agent. Dify provides 50+ built-in tools for AI agents, such as Google Search, DALL·E, Stable Diffusion and WolframAlpha.

**6. LLMOps**: 
  Monitor and analyze application logs and performance over time. You could continuously improve prompts, datasets, and models based on production data and annotations.

**7. Backend-as-a-Service**: 
  All of Dify's offerings come with corresponding APIs, so you could effortlessly integrate Dify into your own business logic.



## Staying ahead

Star Dify on GitHub and be instantly notified of new releases.

![star-us](https://github.com/langgenius/dify/assets/13230914/b823edc1-6388-4e25-ad45-2f6b187adbb4)


#

# DevSecOps Project 

## Pre-requisites to implement this project:

-  AWS EC2 instance (Ubuntu) with instance type t2.large and root volume 29GB.

-  Installation of JAVA
   ```bash
   sudo apt update
   sudo apt install fontconfig openjdk-17-jre
   java -version
   ```

-  Installation of Jenkins
   ```bash
   sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
   https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
   echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
   https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
   sudo apt-get update
   sudo apt-get install jenkins
   ```

-  Before making any changes to the Jenkins configuration, you need to stop the Jenkins server. This can be done using the following command:
   ```bash
   sudo systemctl stop jenkins
   ```

-  Navigate to the directory where the Jenkins configuration file is located:
   ```bash
   cd /etc/default
   ```

-  Inside the `jenkins` file, look for the line that specifies the HTTP port:
   ```bash
   HTTP_PORT=2000
   ```
-  Update the Jenkins Service File
   ```bash
   cd /lib/systemd/system
   ```

-  Open the `jenkins.service` file in your preferred text editor:
   ```bash
   Environment=”JENKINS_PORT=2000"
   ```

-  Reload the Systemd Daemon and Start Jenkins
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl start jenkins
   ```
   
-  Setup Jenkins
   ```bash
   Public-IP:2000 (Jenkins running)
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```
-  Install - Docker, Kubectl, Helm, docker compose using the script 
   ```bash
   ./cluster.sh
   sudo usermod -aG docker $USER && newgrp docker
   minikube start
   ```
- Install trivy
  ```bash
   wget https://github.com/aquasecurity/trivy/releases/download/v0.67.2/trivy_0.67.2_Linux-64bit.deb
   sudo dpkg -i trivy_0.67.2_Linux-64bit.deb
  ```

- SonarQube Server installed
   ```bash
    docker run -itd --name sonarqube-server -p 1234:9000 sonarqube:lts-community
   ```
#
## Steps for Jenkins CI/CD:

1)  Access Jenkins UI and setup Jenkins

![image](https://github.com/DevMadhup/node-todo-cicd/assets/121779953/1eec417e-95ab-4497-ad31-443ecd6b999e)

#

2)  Plugins Installation:

    - Go to <b><i><u>Manage Jenkins</u></i></b>, click on <b><i><u>Plugins</u></i></b> and install all the plugins listed below, we will require for other tools integration:

        - SonarQube Scanner (Version2.16.1)
        - Sonar Quality Gates (Version1.3.1)
        - Docker (Version1.5)
        - Kubernetes
#

3) Go to SonarQube Server and create token

    - Click on <b><i><u> Administration </u></i></b> tab, then <b><i><u> Security </u></i></b>, then <b><i><u> Users </u></i></b> and create Token.
    -  Create a webhook to notify Jenkins that Quality gates scanning is done. (We will need this step later)

        - Go to SonarQube Server, then <b><i><u> Administration </u></i></b>, then <b><i><u> Configuration </u></i></b> and click on <b><i><u> Webhook </u></i></b>, add webhook in below <b>Format</b>:
        > http://<jenkins_url>:2000/sonarqube-webhook/
        
        Example: 

        ```bash
            http://34.207.58.19:2000/sonarqube-webhook/
        ```

        ![image](https://github.com/DevMadhup/node-todo-cicd/assets/121779953/b9ef2301-b8ff-46f4-a457-6345d5e2dab6)


        ![image](https://github.com/DevMadhup/node-todo-cicd/assets/121779953/08a33164-f6a6-4c5d-8a34-7091cf8a5745)

#

4) Go to Jenkins UI <b><i><u> Manage Jenkins </u></i></b>, then <b><i><u> Credentials </u></i></b> and add SonarQube Credentials.

![image](https://github.com/DevMadhup/node-todo-cicd/assets/121779953/f6db72ec-7d8c-4f4c-ae7a-55d99dd20ce9)

#

5) Now, It's time to integrate SonarQube Server with Jenkins, go to <b><i><u> Manage Jenkins </u></i></b>, then <b><i><u> System </u></i></b> and look for <b><i><u> SonarQube Servers </u></i></b> and add SonarQube.

![image](https://github.com/DevMadhup/node-todo-cicd/assets/121779953/54849cb2-fe56-4acd-972d-3057a0eb3deb)

#

6) Go to <b><i><u> Manage Jenkins </u></i></b>, then <b><i><u> tools </u></i></b>, look for <b><i><u> SonarQube Scanner installations </u></i></b> and add SonarQube Scanner.

> Note: Add name as ```Sonar```
![image](https://github.com/DevMadhup/node-todo-cicd/assets/121779953/1fe926f6-a844-42d4-bce4-62193dde6640)

#


### Configure the Jenkins Job test 
- create a jenkins job "test"
- select pipeline
- Pipeline -> SCM --> credentials --> Username and PAT --> Secret name "jenkins-git"
- ALso before triggering the build check make sure to give jenkins and docker permission 
 ```bash
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins
docker ps -a
docker start <sonarqube-container-ID>
minikube status
minikube start
kubectl get nodes
```

### Configure the Jenkins and K8s integration
- We need to create a seperate namespace and create token for our cluster configuration with Jenkins scope
```bash
kubectl create namespace jenkins
kubectl create sa jenkins -n jenkins
kubectl create token jenkins -n jenkins --duration=8760h
kubectl create rolebinding jenkins-admin-binding --clusterrole=admin --serviceaccount=jenkins:jenkins --namespace=jenkins
```
- Now we need to setup the credential in Jenkins so that cluster can communicate with our Jenkins Agent for the builds
```bash
kubectl config view
```
   1. Go to manage jenkins and select cloud --> "kubernetes"
   2. Get the server URL from the above command
   3. Disable http certificate
   4. Type as "secret text" --> add the credential name as "jenkins"
   5. Lastly add the token we created --> Test the connection

### Configure the Jenkins user permission to run the job
- change the default password for jenkins user --> "admin123"
```bash
sudo su
usermod -a -G sudo jenkins
passwd jenkins
```
- Move the kubeconfig file from ubuntu user to jenkins user
```bash
sudo su - jenkins
mkdir -p $HOME/.kube
sudo cp /home/ubuntu/.minikube/profiles/minikube/client.crt /var/lib/jenkins/.kube/
sudo cp /home/ubuntu/.minikube/profiles/minikube/client.key /var/lib/jenkins/.kube/
sudo cp /home/ubuntu/.minikube/ca.crt /var/lib/jenkins/.kube/
sudo cp /home/ubuntu/.kube/config /var/lib/jenkins/.kube
```
- change the path for the kubeconfig file from ubuntu user to jenkins user
``` bash
sudo vi /var/lib/jenkins/.kube/config
```
- We need to change here the config file path for **client-certificate** **client-key** & **certificate-authority**
```bash
users:
   - name: minikube
    user:
       client-certificate: /var/lib/jenkins/.kube/client.crt      —> change it
       client-key: /var/lib/jenkins/.kube/client.key              —> change it
    clusters:
   - cluster:
       certificate-authority: /var/lib/jenkins/.kube/ca.crt     —> change it
```
- change the permission for the kubeconfig file from ubuntu user to jenkins user along with the prmission
```bash
sudo chown jenkins:jenkins /var/lib/jenkins/.kube/client.crt
sudo chown jenkins:jenkins /var/lib/jenkins/.kube/client.key
sudo chown jenkins:jenkins /var/lib/jenkins/.kube/ca.crt
sudo chown jenkins:jenkins /var/lib/jenkins/.kube/config
sudo chmod 600 /var/lib/jenkins/.kube/client.crt
sudo chmod 600 /var/lib/jenkins/.kube/client.key
sudo chmod 600 /var/lib/jenkins/.kube/ca.crt
sudo chmod 600 /var/lib/jenkins/.kube/config
```

- Change the permission for kubernetes config file to run as curent user - jenkins user
```bash
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

- Test as a jenkins user:
```bash
kubectl get nodes
```

## Test the Application:
- Get the application URL by running these commands:
```bash
export POD_NAME=$(kubectl get pods --namespace prod -l "app.kubernetes.io/name=dify,app.kubernetes.io/instance=release,component=proxy" -o jsonpath="{.items[0].metadata.name}")

echo $POD_NAME
```
- Get the port
```bash
export CONTAINER_PORT=$(kubectl get pod --namespace prod $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")

echo $CONTAINER_PORT
```
- Test the frontend exposed on port 8080 (WebApp)
```bash
kubectl --namespace prod port-forward $POD_NAME 8080:$CONTAINER_PORT --address 0.0.0.0 &
```
- http://public-IP:8080
  
<img width="1440" height="649" alt="Screenshot 2025-11-21 at 2 13 07 PM" src="https://github.com/user-attachments/assets/f5a3bd84-6bbd-466e-a700-1490b1a6914b" />

