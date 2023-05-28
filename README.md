# Jenkins-Python-Pipeline-

**Objective**

- The objective of this project is to document my process setting up a simple Jenkins pipeline on an example python project. 


**Steps**:

1. The first thing that I will do is grab the Jenkins image from DockerHub.

```

docker pull jenkins/jenkins:lts-jdk11


```

1. Then I will create a container from the Jenkins image. You can change the port if you have something running on it already. Make sure to save your credentials when they are printed in the terminal. You will need it to setup Jenkins. 

```
docker run -p 8080:8080 -p 50000:50000 --restart=on-failure -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11


```

3. Navigate to the port that you chose. In my case ``http://localhost:8080/``



On completion of setup you will be presented with this screen:


4. Click on create a job 
