pipeline {
    agent any
    
    environment {
        IMAGE_TAG = "${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
    }

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
      
     stage('build and login image') {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernameColonPassword(credentialsId: '0749aa12-736c-4030-84cc-9251547326b4', variable: 'docker-password')]) {
                        sh "docker build -t dapetoo/php-todo:${IMAGE_TAG} ."                 
                    }
                }
            }
        }
      
      stage('Docker Push') {
    	agent any
            steps {
                echo "Login to DockerHub and push the docker image..."
      	        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push dapetoo/php-todo:${IMAGE_TAG}"
                }
            }
        }
  }
}
