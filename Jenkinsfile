pipeline {
  environment{
    COURSIER_CACHE="/home/jenkins/.coursier-cache"
  }
  triggers {
    //pollSCM needed due to https://mohamicorp.atlassian.net/wiki/spaces/DOC/pages/381288449/Configuring+Webhook+To+Jenkins+for+Bitbucket+Git+Plugin
    pollSCM('0 0 1 1 *')
    bitbucketPush()
  }
  stages {
    stage('Notify Stash build starting'){
      steps {
        step([$class: 'StashNotifier'])
      }
    }
    stage('Style Check') {
      steps {
        echo 'Style Check'
        sh 'sbt styleCheck'
      }
    }
    stage('Build') {
      steps {
        echo 'Build'
        sh 'sbt clean compile'
      }
    }
    stage('Dependency Check') {
      steps {
        echo 'Dependency Check'
        sh 'sbt dependencyUpdates'
      }
    }
    stage('Build Docs') {
      steps {
        echo 'Build Docs'
        sh 'sbt doc test:doc'
      }
    }
    stage('Test') {
      steps {
        echo 'Test'
        sh 'sbt test'
      }
    }
  }
}
