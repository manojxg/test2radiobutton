pipeline {
  agent any

  parameters {
    choice(
      name: 'ENV',
      choices: ['Dev', 'Test', 'Stage'],
      description: 'Choose the environment to deploy to'
    )
  }

  stages {
    stage('Deploy') {
      steps {
        script {
          if (params.ENV == 'Dev') {
            echo 'Deploying to Development Environment'
          } else if (params.ENV == 'Test') {
            echo 'Deploying to Testing Environment'
          } else {
            echo 'Deploying to Staging Environment'
          }
        }
      }
    }
  }
}
