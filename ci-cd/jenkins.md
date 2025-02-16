# Jenkins CI/CD CheatSheet

A comprehensive guide covering essential Jenkins commands and configurations for continuous integration and deployment.

## Table of Contents

- [Installation & Setup](#installation--setup)
- [Jenkins CLI](#jenkins-cli)
- [Pipeline as Code (Jenkinsfile)](#pipeline-as-code-jenkinsfile)
- [Managing Jobs](#managing-jobs)
- [Build Triggers](#build-triggers)
- [Artifacts & Workspaces](#artifacts--workspaces)
- [Plugins Management](#plugins-management)
- [Credentials Management](#credentials-management)
- [Distributed Builds](#distributed-builds)
- [Monitoring & Logs](#monitoring--logs)

## Installation & Setup

Download and install Jenkins:

```bash
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update && sudo apt install jenkins
```

Start and enable Jenkins service:

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Get the initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## Jenkins CLI

Connect to Jenkins CLI:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ help
```

Trigger a build from CLI:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ build <job-name>
```

List available jobs:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ list-jobs
```

## Pipeline as Code (Jenkinsfile)

Basic declarative pipeline:

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
```

## Managing Jobs

Create a new job:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ create-job my-job < config.xml
```

Delete a job:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ delete-job my-job
```

## Build Triggers

Trigger a job remotely via API:

```bash
curl -X POST http://localhost:8080/job/my-job/build --user "user:token"
```

Schedule a build at a fixed time:

```groovy
triggers {
    cron('H 2 * * 1-5')
}
```

## Artifacts & Workspaces

Save build artifacts:

```groovy
archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
```

Clean workspace before build:

```groovy
steps {
    deleteDir()
}
```

## Plugins Management

List installed plugins:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ list-plugins
```

Install a new plugin:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ install-plugin git
```

## Credentials Management

Store credentials securely:

```groovy
withCredentials([usernamePassword(credentialsId: 'my-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
    sh 'echo $USER'
}
```

## Distributed Builds

Add a new Jenkins agent:

```bash
java -jar agent.jar -jnlpUrl http://jenkins-master:8080/computer/my-agent/slave-agent.jnlp -secret <secret-key>
```

## Monitoring & Logs

View Jenkins logs:

```bash
tail -f /var/log/jenkins/jenkins.log
```

Monitor system load:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ monitor-memory
```