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
          sh '''
            #!/bin/bash
            aws configure set region ${AWS_DEFAULT_REGION}
            aws configure get region
          '''
        }
      }
    }

    stage('Do something fun') {
      steps {
        script {
          def target = params.Deployment_Target

          echo "Running environment setup and fun.sh for target: ${target}"
          sh """
            #!/bin/bash
            echo 'Listing S3 buckets...'
            aws s3 ls

            echo 'Sourcing environment script and running fun.sh...'
            chmod +x environment/${target}.sh
            chmod +x fun.sh

            source environment/${target}.sh
            env
            pwd
            ls -la
            ./fun.sh
          """
        }
      }
    }
  }

  post {
    always {
      echo "Cleaning up workspace..."
      deleteDir()
    }
  }
}
