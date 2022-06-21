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

                       sh "sudo docker build -t royalt/darey.io:${env.BRANCH_NAME}-${env.BUILD_NUMBER} ."
                }
            }
        }

        stage ('Push Docker Image') {
            steps{
                script {
            sh "sudo docker login -u ${env.username} -p ${env.password}"

            sh "sudo docker push royalt/darey.io:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
            }
          }
        }

        stage ('logout Docker') {
            steps {
                script {

                    sh "sudo docker logout"

                }
            }
        }

    }
}