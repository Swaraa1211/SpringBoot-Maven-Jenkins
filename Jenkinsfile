pipeline {
    agent { label 'swaroopa-jenkins-agent' }
    
    stages {
        stage('Create Git Tag') {
            steps {
                script {
                    def buildTag = "build-${BUILD_NUMBER}"
                    sh "echo Creating tag ${buildTag}"
                    
                    withCredentials([gitUsernamePassword(credentialsId: '66a49eec-98e6-48de-9fd3-01e1d86d03ee',gitTooName:'Default')]) {
                        sh "git config --global user.email 'saiswaroopasaranath1211@gmail.com'"
                        sh "git config --global user.name 'Swaraa1211'"
 
                    sh "git tag ${buildTag}"
                    sh "git push --tags"
                   }
                }
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                sh "sudo docker login -u swaroopa1211 -p dckr_pat_OvhwLThenj_iE0WHdDwzy-KeqYQ"
                sh "sudo docker build -t jenkins_maven ."
                sh "sudo docker tag jenkins_maven:latest swaroopa1211/jenkins_maven:build-${BUILD_NUMBER}"
                sh "sudo docker push swaroopa1211/jenkins_maven:build-${BUILD_NUMBER}"
            
                sh "sudo docker run -p 8081:8081 -d swaroopa1211/jenkins_maven:build-${BUILD_NUMBER}"
            }
        }
    }
}
