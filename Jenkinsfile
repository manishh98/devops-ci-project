pipeline {
    agent any

    environment {
	DOCKER_IMAGE = "manishh98/devops-ci-demo"
	IMAGE_TAG = "${BUILT_NUMBER}"
    }

    stages {
        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$IMAGE_TAG .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
		    credentialsId: 'dockerhub-creds',
                    passwordVariable: 'DOCKER_PASS',
                    usernameVariable: 'DOCKER_USER'
                )]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
            }
        }
    }

	stage('Push Image") {
             steps {
		sh 'docker push $DOCKER_IMAGE:$IMAGE_TAG'
	     }
	}
        
        stage('Run Container'){
   	    steps {
  		sh 'docker run --rm $DOCKER_IMAGE:$IMAGE_TAG'
	    }
	}
    }
