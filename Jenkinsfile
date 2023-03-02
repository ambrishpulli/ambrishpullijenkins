pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ambrishpulli/ambrishpullijenkins.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t ambrishpulli/ambrishpullijenkins .'
                }
            }
        }
        stage('Push image to Docker Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u Ambrishpulli -p ${dockerhubpwd}'

}
                   sh 'docker push ambrishpulli/ambrishpullijenkins'
                }
            }
        }
    }
}