pipeline {
  
  agent {
    node {
      label "jenkins-python-builds"
    }
  }

  stages {

    stage ("Debug") {
      steps {
        sh("printenv")
        script {
          echo("Hello, World!")
          echo("env var:")
          for (envVar in env.getEnvironment()) {
            echo "${envVar.key} -> ${envVar.value}"
          }
        }
      }
    }

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
        sh '''#!/bin/bash
          python3 -m venv venv
          python3 --version
          source venv/bin/activate
          pip install -r requirements.txt
        '''
      }
    }

    stage ("Test") {
      steps {
        sh """#!/bin/bash
              source venv/bin/activate
              pytest
        """
      }
    }
  }

}
