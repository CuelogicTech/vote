pipeline { 
  agent any

  stages {
    stage ('Checkout Code') {
      steps {
        checkout scm
      }
    }
    stage ('Build app') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'gogs', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          // available as an env variable, but will be masked if you try to print it out any which way
          sh 'echo $PASSWORD'
          // also available as a Groovy variable—note double quotes for string interpolation
          echo "$USERNAME"
        }
        sh "echo echo 'Add build commands here'"
      }
    }
    stage('Nexus login') {
        steps {
            sh 'sudo docker login localhost:5000 -u admin -p admin123'
        }
    }
    stage('Docker build') {
        steps {
            sh 'env'
            sh "sudo docker build -t localhost:5000/${env.JOB_NAME}:${env.BUILD_NUMBER}.0 ."
        }
    }
    stage('Docker push') {
        steps {
            sh 'env'
            sh "sudo docker push localhost:5000/${env.JOB_NAME}:${env.BUILD_NUMBER}.0"
        }
    }
  }
}
