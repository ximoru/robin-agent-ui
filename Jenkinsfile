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
    stage('Deploy') {
      steps {
        sh 'gulp clearCurrent && gulp deploy'
      }
    }
    stage('Deliver for staging') {
      when { not { branch 'master' } }
      steps {
        sh 'ssh root@47.104.80.136 rm -rf /home/wwwroot/temp_deploy/current/'
        sh 'ssh root@47.104.80.136 mkdir -p /home/wwwroot/temp_deploy'
        sh 'scp -r release/current root@47.104.80.136:/home/wwwroot/temp_deploy/current/'
        sh 'ssh root@47.104.80.136 "rm -rf /home/wwwroot/robin-agent-dev.laralab.org/* && mv /home/wwwroot/temp_deploy/current/* /home/wwwroot/robin-agent-dev.laralab.org/"'
        dingTalk accessToken: 'd856d34f014618d97672ed967de530b55a4f5d1d754e7c7b3234c6dceeec2250', imageUrl: 'https://www.iconsdb.com/icons/preview/guacamole-green/approval-xl.png', jenkinsUrl: 'http://ci.laralab.org', message: '代理系统 UAT 更新成功', notifyPeople: ''
      }
    }
  }
}
