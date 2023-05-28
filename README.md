# Jenkins-Python-Pipeline-

**Objective**

- The objective of this project is to document my process setting up a simple Jenkins pipeline on an example python project to automate testing. I might also add a github webhook in the future to trigger on commits to the example repo. 


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
![Screenshot from 2023-05-28 11-48-22](https://github.com/josiah34/Jenkins-Python-Pipeline-/assets/25124463/94386d21-1041-4df1-9946-acd820f64388)


4. Click on create a new item on the left.

5. Select Pipeline in the menu. Give the pipeline a name then click ok.
6. Add a description.
7. Go down to the pipeline defintion to start coding the pipeline in groovy. You can click on pipeline Syntax to assist in generating code for common pipeline steps. In this case I used git, checkout and sh(Shell script) 
8. This is the groovy script I wrote within my defintion. 
9. 
