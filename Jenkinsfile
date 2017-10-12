pipeline {
  agent any
  stages {
    stage(' Build Registrar') {
      steps {
        git(url: 'https://github.com/sniperd/opsworks-dev-demo.git', branch: 'master', credentialsId: 'jenkins')
        sh 'echo \'hi\''
        archiveArtifacts 'bleh'
      }
    }
    stage('Execute tests') {
      parallel {
        stage('Integration Tests') {
          steps {
            sh 'echo \'test\''
          }
        }
        stage('Unit Testing') {
          steps {
            sh 'echo \'unit tests\''
          }
        }
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
      try {
        currentBuild.result = "SUCCESS"
        steps {
          sh 'echo \'deploy prod\''
        }
      } catch (err) {
        currentBuild.result = "FAILURE"
        throw err
      }
    }
  }
}
