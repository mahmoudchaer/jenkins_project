pipeline {
  agent any

  environment {
    VIRTUAL_ENV = 'venv'
  }

  stages {
    stage('Setup') {
      steps {
        bat '''
          python -m venv %VIRTUAL_ENV%
          call %VIRTUAL_ENV%\\Scripts\\activate
          python -m pip install --upgrade pip
          pip install -r requirements.txt
        '''
      }
    }

    stage('Lint') {
      steps {
        bat '''
          call %VIRTUAL_ENV%\\Scripts\\activate
          flake8 app.py
        '''
      }
    }

    stage('Test') {
      steps {
        bat '''
          call %VIRTUAL_ENV%\\Scripts\\activate
          pytest
        '''
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying application...'
      }
    }
  }

  post {
    always {
      cleanWs()
    }
  }
}
