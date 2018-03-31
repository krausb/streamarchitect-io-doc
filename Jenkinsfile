pipeline {
  environment{
    COURSIER_CACHE="/var/jenkins_home/.coursier-cache"
  }
  agent {
    label 'master'
  }
  triggers {
    //pollSCM needed due to https://mohamicorp.atlassian.net/wiki/spaces/DOC/pages/381288449/Configuring+Webhook+To+Jenkins+for+Bitbucket+Git+Plugin
    pollSCM('0 0 1 1 *')
  }
  stages {
    stage('Build') {
      steps {
        echo 'Build'
        sbt('clean compile paradox')
      }
    }
  }
}
