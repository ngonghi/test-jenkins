pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Git Checkout') {
            steps {
                echo '> Checking out deploy branch ...'
                sh 'git fetch origin'
                sh 'git checkout params.branch'
                sh 'git pull origin params.branch'
            }
        }
        stage('Build') { 
            steps {
                sh 'test.sh'
                sh 'npm install' 
            }
        }
    }
}
