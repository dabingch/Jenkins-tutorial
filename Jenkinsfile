pipeline {
  agent any

  triggers {
    // Poll GitHub every 5 minutes (with Jenkins’ H-scatter)
    pollSCM('H/5 * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        // pulls from the branch that triggered the build
        checkout scm
      }
    }

    stage('Install & Test') {
      steps {
        // create venv, install, run pytest
        sh '''
          python3 -m venv venv
          . venv/bin/activate
          pip install -r requirements.txt
          pytest
        '''
      }
    }
  }

  post {
    always {
      // print a clear “done” message to the Jenkins console
      echo "=== CI/CD PROCESS COMPLETED ==="
    }
  }
}

