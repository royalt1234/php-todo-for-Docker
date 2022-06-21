pipeline {
    agent any

    stages {

        stage('Initial Cleanup') {
            steps {
            dir("${WORKSPACE}") {
              deleteDir()
            }
          }
        }

        stage ('Checkout Repo'){
            steps {
            git branch: 'main', url: 'https://github.com/royalt1234/php-todo-for-Docker.git'
      }
        }

        stage ('Build Docker Image') {
            steps {
                script {

                       sh "docker build -t royalt/darey.io:${env.BRANCH_NAME}-${env.BUILD_NUMBER} ."
                }
            }
        }

        stage ('Run Container') {
            steps {
                script {

                       sh "docker run --network php -p 8087:8000 -d royalt/darey.io:${env.BRANCH_NAME}-${env.BUILD_NUMBER} ."
                }
            }
        }

        stage ('Test-Stage-Curl') {
            steps {
                script {

                    sh "curl --version"
                    sh  "curl -I http://3.95.65.147:8087"
                }
            }
        }


        stage ('Push Docker Image') {
            steps{
                script {
            sh "docker login -u ${env.username} -p ${env.password}"

            sh "docker push royalt/darey.io:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
            }
          }
        }


        stage ('Clean Up') {
            steps{
                script {

            sh "docker system prune -af"

          }
        }


        stage ('logout Docker') {
            steps {
                script {

                    sh "docker logout"

                }
            }
        }

    }
}