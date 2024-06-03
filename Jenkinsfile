pipeline {
  
  agent {
    node {
      label "jenkins-python-builds"
    }
  }

  stages {

    stage ("Checkout") {
      steps {
        checkout([$class: 'GitSCM',
                  branches: [[name: 'main']],
                  doGenerateSubmoduleConfigurations: false])
      }
    }
    
    stage ("Build") {
      steps {
        sh "python3 -m venv venv"
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
