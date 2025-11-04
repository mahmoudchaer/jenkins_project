pipeline {
  agent any

  environment {
    VIRTUAL_ENV = 'venv'
  }

  stages {
    stage('Setup') {
      steps {
        dir('jenkins_project') {
          sh '''
            if [ ! -d "$VIRTUAL_ENV" ]; then
              python3 -m venv "$VIRTUAL_ENV"
            fi
            . "$VIRTUAL_ENV/bin/activate"
            pip install --upgrade pip
            pip install -r requirements.txt
          '''
        }
      }
    }

    stage('Lint') {
      steps {
        dir('jenkins_project') {
          sh '''
            . "$VIRTUAL_ENV/bin/activate"
            flake8 app.py
          '''
        }
      }
    }

    stage('Test') {
      steps {
        dir('jenkins_project') {
          sh '''
            . "$VIRTUAL_ENV/bin/activate"
            pytest
          '''
        }
      }
    }

    stage('Deploy') {
      steps {
        script {
          echo 'Deploying application...'
        }
      }
    }
  }

  post {
    always {
      cleanWs()
    }
  }
}

