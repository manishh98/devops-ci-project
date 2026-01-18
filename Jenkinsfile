pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-ci-demo:1.0 .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run --rm devops-ci-demo:1.0'
            }
        }
    }
}

