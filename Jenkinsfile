pipeline{
    agent any
    stages{
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build -t pereeee04/hiring:0.0.2 ."
            }
        }
        stage('Docker Push'){
            steps{
                sh "docker login -u pereeee04 -p xxxxx"
                sh "docker push pereeee04/hiring:0.0.2"
            }
        }
    }
}
