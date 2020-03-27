pipeline {
    agent any
    properties([
        parameters([
            gitParameter(branch: '',
                         branchFilter: 'origin/(.*)',
                         defaultValue: 'master',
                         description: '',
                         name: 'BRANCH',
                         quickFilterEnabled: false,
                         selectedValue: 'NONE',
                         sortMode: 'NONE',
                         tagFilter: '*',
                         type: 'PT_BRANCH')
        ])
    ])
    node {
        git branch: "${params.BRANCH}", url: 'https://github.com/ngonghi/test-jenkins.git'
    }
    stages {
        stage('Build docker image') {
            steps {
                echo '> Building the docker images ...'
                sh 'docker-compose -f /home/kasika-docker/docker-composer.kasika_db_manager_ci.yml up --exit-code-from kasika_db_manager_app --remove-orphans kasika_db_manager_app'
            }
        }
        stage('Install vendor') {
            steps {
                echo '> Install vendor ...'
                sh 'docker-compose exec -w /var/www/html/kasika-db-manager -T kasika_db_manager_app npm install'
                sh 'docker-compose exec -w /var/www/html/kasika-db-manager -T kasika_db_manager_app npm run production'
                sh 'docker-compose exec -w /var/www/html/kasika-db-manager -T kasika_db_manager_app composer install'
            }
        }
        stage('Push to server') {
            steps {
                echo '> Pushing source to server ...'
            }
        }
        stage('Destroy') {
            steps {
                echo '> Destroying the docker artifacts ...'
                sh 'docker-compose -f /home/kasika-docker/docker-composer.kasika_db_manager_ci.yml down'
            }
        }
    }
}


