pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/your-repo-name.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop azure || true
                docker rm azure || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi amazon || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t amazon .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 6060:8080 --name azure amazon'
            }
        }
    }
}
