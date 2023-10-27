pipeline {
    agent {label 'swaroopa-jenkins-agent'}
    
    stages {
        stage('Build and Test') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Create Git Tag') {
            steps {
                script {
                    def buildTag = "build-${BUILD_NUMBER}"
                    sh "echo Creating tag ${buildTag}"
                    sh "git tag -a ${buildTag} -m 'Jenkins build ${BUILD_NUMBER}'"
                    sh "git push origin ${buildTag}"
                }
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                sh "docker login -u swaroopa1211 -p dckr_pat_OvhwLThenj_iE0WHdDwzy-KeqYQ"
                sh "docker build -t jenkins_maven ."
                sh "docker tag jenkins_maven:latest my-registry/jenkins_maven:build-${BUILD_NUMBER}"
                sh "docker push swaroopa1211/jenkins_maven:build-${BUILD_NUMBER}"
                sh "docker run -p 8081:8081 -d swaroopa1211/jenkins_maven:build-${BUILD_NUMBER}"
            }
        }
 
    }
}