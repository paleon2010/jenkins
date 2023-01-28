pipeline {
  agent any
  stages {
    stage('Print Message') {
      steps {
        echo 'Build Demo Application'
      }
    }

    stage('Shell Script') {
      parallel {
        stage('Shell Script') {
          steps {
            sh 'sh run_build_script.sh'
          }
        }

        stage('linux test') {
          steps {
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('windows test') {
          steps {
            echo 'Run Windows tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok to deploy to production?'
      }
    }

    stage('Deploy Production') {
      post {
        always {
          archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
        }

        failure {
          emailext(subject: 'Demoapp build failure', to: 'ci-team@example.com', body: 'Build failure for demoapp Build ${env.JOB_NAME} ')
        }

      }
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
}