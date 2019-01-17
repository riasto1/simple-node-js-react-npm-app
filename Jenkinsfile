pipeline {
  agent {
    docker {
      args '-p 3000:3000'
      image 'node:6-alpine'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Delivery') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using wrbsite'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
  environment {
    npm_config_cache = 'npm_cahce'
  }
}