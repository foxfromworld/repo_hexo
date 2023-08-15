---
title: Creating my first Jenkins Pipeline
date: 2023-08-11 13:51:05
tags: [Jenkins, Ubuntu, Pipeline]
categories: Jenkins
---

### Install the Docker Pipeline plugin through the Manage Jenkins > Plugins page

Search for "Docker Pipeline"

![](plugin.PNG)

### After installing the plugin, restart Jenkins so that the plugin is ready to use

Go "Dashboard" and click on "New Item".

Enter an item name and choose "Pipeline", then click on "OK".

![](buildntest.PNG)

Here is the example I used for testing the pipeline.

https://github.com/foxfromworld/python-test

First, I chose "Hello World" for my "Pipeline script".

Then, click on "Pipeline Syntax" to find the script for "checkout", paste your repo URL here, and click on "Generate Pipeline Script".

![](syntax.PNG)

The script will be like:

```
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/foxfromworld/python-test.git']])
            }
        }
    }
}
```

Go back to the dashboard, click on "Build Now", you can see the result.

![](firstbuild.PNG)

After successfully check out the code, now we can try to build and test the project.

Click on "Pipeline Syntax" to find the script for "sh: Shell Script",

![](build.PNG)

```
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/foxfromworld/python-test.git']])
            }
        }
        stage('Build') {
            steps {
                sh 'python3 countOdds.py'
            }
        }
    }
}
```

Click on "Build Now" and you can see the message.

![](built.PNG)

Finally, modify the script to add the test stage.

```
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/foxfromworld/python-test.git']])
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/foxfromworld/python-test.git'
                sh 'python3 countOdds.py'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }        
    }
}
```

Opps, I got this when running the test stage.

![](fail.PNG)

```
+ /usr/bin/python3 -m pytest
/usr/bin/python3: No module named pytest
```

Try the new script below to install pytest and specify the python3 version. (Once I couldn't find the pytest even after the installation then I realized it might have been a different python version.) It fixed the problem.

```
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/foxfromworld/python-test.git']])
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/foxfromworld/python-test.git'
                sh 'python3 countOdds.py'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                
                withEnv(["HOME=${env.WORKSPACE}"]) {
                    sh '/usr/bin/python3 -m pip install --upgrade pip'
                    sh 'pip install -r requirements.txt'
                    sh 'python3 --version'
                    sh '/usr/bin/python3.10 -m pytest'
                }
            }
        }        
    }
}
```

![](test.PNG)