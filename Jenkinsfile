pipeline {
  agent any

  environment {
    ROLE_ARN     = 'arn:aws:iam::773493560304:root'
    SESSION_NAME = 'jenkins-session'
    AWS_REGION   = 'eu-west-1'
  }

  stages {
    stage('Launch EC2') {
      steps {
        sh '''
          #!/bin/bash

          echo "Assuming role: $ROLE_ARN"
          CREDS=$(aws sts assume-role \
            --role-arn "$ROLE_ARN" \
            --role-session-name "$SESSION_NAME" \
            --region "$AWS_REGION" \
            --output json)

          ACCESS_KEY=$(echo $CREDS | jq -r '.Credentials.AccessKeyId')
          SECRET_KEY=$(echo $CREDS | jq -r '.Credentials.SecretAccessKey')
          SESSION_TOKEN=$(echo $CREDS | jq -r '.Credentials.SessionToken')

          echo "Launching EC2 instance..."
          aws ec2 run-instances \
            --image-id ami-0bc691261a82b32bc \
            --instance-type t2.micro \
            --region "$AWS_REGION" \
            --count 1 \
            --iam-instance-profile Name=YourEC2Profile \
            --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=Jenkins-Launch}]' \
            --cli-input-json file://launch-config.json \
            --output json \
            --access-key "$ACCESS_KEY" \
            --secret-key "$SECRET_KEY" \
            --session-token "$SESSION_TOKEN"
        '''
      }
    }
  }
}
