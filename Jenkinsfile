pipeline {
  agent any
  options {
    disableConcurrentBuilds()
    timeout(time: 5, unit: 'MINUTES')
    buildDiscarder(logRotator(numToKeepStr: '100'))
    timestamps()
  }

  stages {
    stage ('Prepare') {
      steps {
        checkout scm
      }
    }
    stage ('Verify') {
      steps {
        sh 'grep workaround-bindep playbooks/base/pre.yaml'
      }
    }
  }
  post {
    failure {
      mattermostSend color: "danger", channel: "#infrastructure", message: "[Software Factory config](https://github.com/TinxHQ/wazo-production-sf-config) is missing workaround-bindep on master - [Job :nuke:](${JOB_URL})"
    }
  }
}
