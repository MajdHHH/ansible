pipeline {
  agent any
  triggers { githubPush() }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Run maintenance') {
      steps {
        sshagent(credentials: ['ansible-key']) {
          sh '''
            set -e
            cd "$WORKSPACE"
            ls -la
            ansible-playbook -i inventory maintenance.yml
          '''
        }
      }
    }
  }
}

