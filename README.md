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


<details>
  <summary>Jenkins File Code</summary>

  ```

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/josiah34/Jenkins-Python-Pipeline-.git']])
            }
        }
        stage('Build') {
            steps {
               git branch: 'main', url: 'https://github.com/josiah34/Jenkins-Python-Pipeline-.git'
               sh 'python3 operations.py'
            }
        }
        stage('Test') {
            steps {
               git branch: 'main', url: 'https://github.com/josiah34/Jenkins-Python-Pipeline-.git'
               sh 'python3 -m pytest -v'
            }
            
            
        }
    }
    
    
}

```
</details>

10. This pipeline will produce two errors in the Build and Test stages. The docker container that Jenkins is running on does not have Python3 abd pytest installed on it. To fix this we need to go into the Jenkins container and install both use the following commands:

Interact with Docker container with shell:

```docker exec -it -u 0 CONTAINER_ID /bin/bash```

Update the packages:
```apt-get update```

Install Python3: 
```sudo apt install python3```

Install Pip:
```sudo apt install python3-pip```

Install Pytest:
```pip install pytest```


Once those command are executed we are ready to run the pipelines.
![jenkins-python-pipeline](https://github.com/josiah34/Jenkins-Python-Pipeline-/assets/25124463/a4c4f5e6-074c-4945-8514-44cd88970262)





