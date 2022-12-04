pipeline {
    agent any


  stages {

     stage("Initial cleanup") {
          steps {
            dir("${WORKSPACE}") {
              deleteDir()
            }
          }
        }
  
    stage('Checkout Git') {
      steps {
            git branch: 'dapetoo-docker-build', credentialsId: 'a43263cb-ef76-4719-bdaa-7f8f4e36cf48', url: 'https://github.com/scholarship-task/php-todo'
      }
    }

    stages {
        stage('Test') {
            steps {
                sh 'node --version'
                sh 'svn --version'
            }
        }
    }

    stage('Login to DockerHub') {
      steps {
          sh 'docker login -u dapetoo -p ${docker_password}'
      }
    }
      
  }
}
