pipeline {
  agent any

  environment {
    ROLE_ARN     = 'arn:aws:iam::773493560304:role/Super_user'
    SESSION_NAME = 'jenkins-session'
    AWS_REGION   = 'eu-west-1'
  }

  stages {
    stage('Launch EC2') {
      steps {
        sh '''
        
          echo "Launching EC2 instance..."
          aws ec2 run-instances \
            --image-id ami-0bc691261a82b32bc \
            --instance-type t2.micro \
            --region "$AWS_REGION" \
            --count 1 \
            --iam-instance-profile Name=Super_user \
            --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=Jenkins-Launch}]' \
        '''
      }
    }
  }
}
