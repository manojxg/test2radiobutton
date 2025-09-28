properties([
  parameters([
    choice(name: 'Deployment_Target', choices: ['AWS-SS-Dev'], description: 'Choose deployment environment'),
    string(name: 'Change_Number', defaultValue: '', description: 'Enter a ServiceNow Change Number if appropriate')
  ])
])

pipeline {
  agent any

  options {
    ansiColor('xterm')
  }

  environment {
    AWS_DEFAULT_REGION = 'eu-west-1'
  }

  stages {
    stage('Pre-Reqs') {
      steps {
        script {
          echo "Setting AWS region"
          sh 'aws configure set region eu-west-1'
          sh 'aws configure get region'
        }
      }
    }

    stage('Do something fun') {
      steps {
        script {
          def target = params.Deployment_Target
          echo "Running environment setup and fun.sh"
          sh """
            source .environment/${target}.sh
            env
            pwd
            ls -la
            chmod +x ./fun.sh
            ./fun.sh
          """
        }
      }
    }
  }

  post {
    always {
      deleteDir()
    }
  }
}
