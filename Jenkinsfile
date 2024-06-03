pipeline {
  
  agent {
    node {
      label "jenkins-python-builds"
    }
  }

  stages {

    stage ("Checkout") {
      steps {
        script {
          def repoUrl = params.GIT_URL
          checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: repoUrl]]])
        }
      }
    }
    
    stage ("Build") {
      steps {
        sh "python3 --version"
        sh "python3 -m venv venv"
        sh '''#!/bin/bash
          source venv/bin/activate
          pip install -r requirements.txt
        '''
      }
    }
    stage ("Test") {
      steps {
        sh "pytest"
      }
    }
  }
}
