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
            git branch: 'main', url: 'https://github.com/uzukwujp/php-todo.git'
      }
        }

        stage ('Build Docker Image') {
            steps {
                script {

                       sh "docker build -t uzukwujp/php-todo:${env.BRANCH_NAME}-${env.BUILD_NUMBER} ."
                }
            }
        }

        stage ('Push Docker Image') {
            steps{
                script {
            sh "docker login -u ${env.username} -p ${env.password}"

            sh "docker push uzukwujp/php-todo:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
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