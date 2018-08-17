pipeline {
  agent any
  stages {
    stage('Information') {
      steps {
        sh 'node -v'
        sh 'npm -v'
        sh 'gulp -v'
      }
    }
    stage('Dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh 'gulp && gulp release'
      }
    }
    stage('Deliver for staging') {
      when { not { branch 'master' } }
      steps {
        sh 'gulp deployToDev'
      }
    }
  }
}
