pipeline{
    agent any
    stages {
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build -t abdulgayaz123/hiring:0.0.2 ."
            }
        }
        stage('Docker Push'){
            steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'hubPWD')]) {
                    sh "docker login -u pereeee04 -p ${hubPWD}"
                    sh "docker push abdulgayaz123/hiring:0.0.2"
                }
            }
        }
        stage('Docker Deploy') {
            steps {
                sshagent(['docker-host']) {
                    sh "ssh ec2-user@172.31.41.78 docker run -d -p 8080:8080 --name prerana pereeee04/hiring:0.0.2"
                }
            }
        }
    }
}
