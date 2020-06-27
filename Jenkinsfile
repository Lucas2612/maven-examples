pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'hello world!'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Linux test') {
      parallel {
        stage('Linux test') {
          steps {
            echo 'run linux test'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('windows test') {
          steps {
            echo 'windows test'
          }
        }

      }
    }

    stage('Deploying stage') {
      steps {
        echo 'Deploy stage'
        input 'Ok to deploy to production?'
      }
    }

    stage('Deploy production') {
      steps {
        echo 'deloy prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}