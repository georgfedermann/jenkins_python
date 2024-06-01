pipeline {
  
  agent {
    node {
      label "jenkins-python-builds"
    }
  }

  stages {
    
    stage ("Build") {
      steps {
        sh "python -m venv venv"
        sh "source venv/bin/activate"
        sh "pip install -r requirements.txt"
      }
    }
    stage ("Test") {
      steps {
        sh "pytest"
      }
    }
    
  }
  
}
