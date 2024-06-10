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
          println("Hello, World!")
          println("env var:")
          println(env)
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
