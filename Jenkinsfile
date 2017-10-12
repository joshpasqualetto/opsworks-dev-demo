pipeline {
  agent any
  stages {
    stage(' Build Registrar') {
      steps {
        git(url: 'https://github.com/sniperd/opsworks-dev-demo.git', branch: 'master', credentialsId: 'jenkins')
          sh 'echo \'hi\''
      }
    }
    stage('Execute tests') {
      steps {
        sh 'echo \'unit tests\''
      }
    }
    stage('Deploy Development') {
      steps {
        sh 'echo \'deploy dev\''
      }
    }
    stage('User Acceptance') {
      steps {
        input(message: 'Deploy to QA?', id: 'deploy_to_qa', ok: 'yes')
      }
    }
    stage('Deploy QA') {
      steps {
        sh 'echo \'Deploy QA\''
      }
    }
    stage('Manual Acceptance') {
      steps {
        sh 'echo \'deploy to prod\''
      }
    }
    stage('Deploy Prod') {
      steps {
        sh 'echo \'deploy prod\''
      }
    }
  }
  post {
    success {
      echo 'yes'
    }
    failure {
      echo 'no'
    }
  }
}
