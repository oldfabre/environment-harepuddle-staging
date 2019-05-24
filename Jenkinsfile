pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    DEPLOY_NAMESPACE = "jx-staging"
    CHART_REPOSITORY = "http://fr1cslfcglo0082.misys.global.ad"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('env') {
	    sh "echo Hi"
            sh 'jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm apply'
          }
        }
      }
    }
  }
}
