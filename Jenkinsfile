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
                withCredentials([string(credentialsId: 'docker-hub', variable: 'hubbpwd')]) {
                    sh "docker login -u abdulgayaz123/ -p ${hubbpwd}"
                    sh "docker push abdulgayaz123/hiring:0.0.2"
                }
            }
        }
        stage('Docker Deploy') {
            steps {
                sshagent(['docker-host']) {
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.40.72 docker run -d -p 8080:8080 --name abbu abdulgayaz123//hiring:0.0.2"
                }
            }
        }
    }
}
