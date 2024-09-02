pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'yuvalshaul/my_clock'
    }
    stages { 
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'echo Build number is: $BUILD_NUMBER'
                sh 'docker build . -t $DOCKER_IMAGE'
                withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
                sh 'docker push $DOCKER_IMAGE'
            }
        }
        stage('Moshe') {
            when {
                branch 'moshe'
            }
            steps {
                echo 'Running Moshe-specific steps...'
            }
        }
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying...'
                // Add deployment steps here
            }
        }
    }
}

