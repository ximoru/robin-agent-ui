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
        sh 'gulp && gulp clearCurrent && gulp release'
      }
    }
    stage('Deliver for staging') {
      when { not { branch 'master' } }
      steps {
        sh 'ssh root@47.104.80.136 rm -rf /home/wwwroot/temp_deploy/current/'
        sh 'ssh root@47.104.80.136 mkdir -p /home/wwwroot/temp_deploy'
        sh 'scp -r release/current root@47.104.80.136:/home/wwwroot/temp_deploy/current/'
        sh 'ssh root@47.104.80.136 "rm -rf /home/wwwroot/robin-agent-dev.laralab.org/* && mv /home/wwwroot/temp_deploy/current/* /home/wwwroot/robin-agent-dev.laralab.org/"'
      }
    }
  }
}
