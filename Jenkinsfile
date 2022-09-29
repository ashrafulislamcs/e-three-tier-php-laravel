pipeline {
    agent {label "app" } 
    tools {
        maven 'Maven'
    }
    environment {
        docker_id = "sanjoydeb0007"
        docker_pass = "dckr_pat_XmerjW_iWl7qYTILI7GO5rIFgSk"
    }
    stages {
        stage ('git hub integration') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub', url: 'https://github.com/sanjoy-deb-devops/e-three-tier-php-laravel']]])
            }
        }
        stage ('docker login') {
            steps {
                sh 'docker login -u $docker_id -p $docker_pass'
                sh 'docker stop $(docker ps -a -q)'
                sh 'docker rm $(docker ps -a -q)'
            }
        }
        stage ('docker build') {
            steps {
                sh 'docker-compose build app'
                sh 'docker-compose up -d'
                sh 'docker ps'
            }
        }
        stage ('application run') {
            steps {
                sh 'docker-compose exec -T app ls -la'
                sh 'docker-compose exec -T app rm -rf vendor composer.lock'
                sh 'docker-compose exec -T app composer install'
                sh 'docker-compose exec -T app php artisan key:generate'
                sh 'docker-compose exec -T app php artisan migrate'
            }
        }
        stage ('docker tag change or rename') {
            steps {
                sh 'docker tag travellist sanjoydeb0007/test-rnd'
            }
        }
        stage ('docker push') {
            steps {
                sh 'docker push sanjoydeb0007/test-rnd:latest'
            }
        }
         stage ('docker logout session') {
            steps {
                sh 'docker logout'
            }
        }
    }
}

