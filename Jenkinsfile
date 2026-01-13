pipeline{
  agent any

  stages{
    
    stage('Checkout') {
      steps {
        echo 'Fetching source code'
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Build process is going on'
        bat 'echo Build completed successfully!'
        
      }
    }
    
    stage('Validation Check') {
      steps {
        echo 'Validating project readiness'
        bat '''
        findstr READY=true check.txt > nul
        if errorlevel 1 (
              echo Validation Failed
              exit 1
        ) else (
              echo Validation Passed
        )
        '''
        
      }
    }

    stage ('Manager Approval') {
      steps {
        input message: 'Approve deployment?', ok: 'Approve'
      }
    }

    stage ('Ready for Deplotment'){
      steps {
        echo 'Deployment approved and ready'
      }
    }
  }
    post {
      success {
        echo 'Pipeline completed successfully'
      }
      failure {
        echo 'Pipeline failed- code blocked'
    }
  }
}
