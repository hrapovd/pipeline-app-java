pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build Demo Application'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run Linux tests'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows Tests') {
          steps {
            echo 'Run Windows tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok to deploy to product'
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      echo 'Something went wrong'
    }

  }
}