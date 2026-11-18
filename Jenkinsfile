pipeline {
    agent {
        label 'web-agent'
    }

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Code downloaded from GitHub'
            }
        }

        stage('Validate') {
            steps {
                sh 'test -f site/index.html'
                sh 'test -f site/style.css'
                echo 'Website files validated'
            }
        }

        stage('Deploy') {
            steps {
                sh 'rsync -av --delete site/ /var/www/jenkins-site/'
                echo 'Website deployed successfully'
            }
        }

        stage('Verify') {
            steps {
                sh 'curl -fsS http://localhost/ >/dev/null'
                echo 'Website verification successful'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}
