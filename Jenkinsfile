pipeline { 
  agent any

  environment {
    NEXUS_URL = credentials('nexus_url')
    NEXUS = credentials('nexus')
  }

  stages {
    stage ('Checkout Code') {
      steps {
        checkout scm
      }
    }
    stage ('Build app') {
      steps {
        sh "echo 'Write build commands here'"
      }
    }
    stage('Nexus login') {
        steps {
            sh "sudo docker login $NEXUS_URL -u $NEXUS_USR -p $NEXUS_PSW"
        }
    }
    stage('Docker build') {
        steps {
            sh 'env'
            sh "sudo docker build -t $NEXUS_URL/${env.JOB_NAME}:${env.BUILD_NUMBER} ."
        }
    }
    stage('Docker push') {
        steps {
            sh 'env'
            sh "sudo docker push $NEXUS_URL/${env.JOB_NAME}:${env.BUILD_NUMBER}"
        }
    }
  }
}
