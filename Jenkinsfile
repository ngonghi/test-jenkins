pipeline {
    agent {
        docker {
            image 'nghinv91:php70:0.1'
        }
    }
    parameters {
        gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
    }
    stages {
        stage('Example') {
          steps {
            git branch: "${params.BRANCH}", url: 'https://github.com/ngonghi/test-jenkins.git'
          }
        }
        stage('Build docker image') {
            steps {
                sh 'php -v'
            }
        }
    }
}


