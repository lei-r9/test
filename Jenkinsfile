pipeline {
  agent {
    node {
      label 'AGENT_LABEL'
    }

  }
  stages {
    stage('Prepare') {
      steps {
        p4sync '1'
        sh 'echo hello'
      }
    }

    stage('BuildEditor') {
      environment {
        MainBuilder = ''
        ClientBuilder = ''
        ServerBuilder = ''
      }
      parallel {
        stage('BuildEditor') {
          steps {
            p4sync '1'
            sh 'echo Build Editor'
            sh 'echo Cook ALLPlatform'
            sh 'echo wait for sub builders'
          }
        }

        stage('BuildClient') {
          steps {
            p4sync '1'
            sh 'echo Build Client'
            sh 'echo source stamp'
            sh 'echo transfer to Main builder'
          }
        }

        stage('BuildServer') {
          steps {
            p4sync '1'
            sh 'echo Build Server'
            sh 'echo transfer to main builder'
            sh 'echo source stamp'
          }
        }

      }
    }

    stage('Stage') {
      steps {
        sh 'echo stage builds'
      }
    }

    stage('Symbol') {
      parallel {
        stage('Symbol Local') {
          steps {
            sh 'echo Symbol local'
          }
        }

        stage('Symbol Sentry') {
          steps {
            sh 'echo Symbol Sentry'
          }
        }

        stage('Publish Shift') {
          steps {
            sh 'echo Publish Shift'
          }
        }

      }
    }

    stage('finish') {
      steps {
        sh 'echo no op'
      }
    }

  }
}