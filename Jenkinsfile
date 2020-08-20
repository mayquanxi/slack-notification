pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'echo "this is stage Build"'
      }
    }
    stage('Test') {
      steps {
          sh 'echo "this is stage Test"'
          sh 'whoami'
      }
    }
  }
  post {
    
    success {
      echo 'This will run only if successful'
      slackSend channel: '#general', 
                          message: "This will run only if successful: ${env.JOB_NAME} and ${env.BUILD_URL}"
    }
    always {
      echo 'This is always run'
      deleteDir()
      slackSend channel: '#jenkins', 
                          message: "This is always run"
    }
    failure {
      echo 'This will run only if failed'
      slackSend channel: '#jenkins', 
                          message: "This will run only if failed"
      }
    unstable {
      echo 'This will run only if the run was marked as unstable'
      slackSend channel: '#jenkins', 
                          message: "This will run only if the run was marked as unstable"
    }
  }
}
