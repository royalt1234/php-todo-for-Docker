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

                       sh "docker build -t royalt1234/php-todo-for-Docker:${env.BRANCH_NAME}-${env.BUILD_NUMBER} ."
                }
            }
        }

        stage ('Push Docker Image') {
            steps{
                script {
            sh "docker login -u ${env.username} -p ${env.password}"

            sh "docker push royalt1234/php-todo-for-Docker:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
            }
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