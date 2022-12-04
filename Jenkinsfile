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
  
    stage('Checkout SCM') {
      steps {
            git branch: 'dapetoo-docker-build', url: 'https://github.com/darey-devops/php-todo.git'
      }
    }


    stage('Install Dependencies') {
      steps {
          echo "Test"
      }
    }
      
  }
}
