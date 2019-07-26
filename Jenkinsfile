pipeline {
  agent any
  tools {
        gradle 'GRADLE_HOME'
        jdk 'JAVA_HOME'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh ' gradle clean'
        sh 'gradle build'
      }
    }
    stage('Package') {
      steps {
        sh 'serverless package'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        
}
        sh 'serverless deploy'
      }
    }
  }
}
