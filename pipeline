pipeline {
    agent {
        label 'TEST NODE'
    }
    parameters {
        string(name: 'JENKINS_DOCKER_MESSAGE', defaultValue: 'hello')
        string(name: 'JENKINS_IMAGE_NAME', defaultValue: 'dockerjenkins')
        string(name: 'JENKINS_IMAGE_TAG', defaultValue: 'test')
    }
    stages {
        stage('Build Docker image') {
            steps {
                git branch: 'master', url: 'https://github.com/ivshkvs/jenkins.git'
                sh "sudo docker build -t \"$JENKINS_IMAGE_NAME:$JENKINS_IMAGE_TAG\" --build-arg 
DOCKER_MESSAGE=\"$JENKINS_DOCKER_MESSAGE\" ."
            }
        }
        stage('Run Docker container') {
            steps {
                sh "sudo docker run -p 8082:80 -d --name dockerjenkins --rm 
\"$JENKINS_IMAGE_NAME:$JENKINS_IMAGE_TAG\""
            }
        }
    }
}

