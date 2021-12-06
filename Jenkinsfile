pipeline {
  agent any
  stages {
    stage('Prepare calculation-offer-service') {
      steps {
        dir(path: 'source/calculation-offer-service/CalculationServiceAPISolution') {
          sh 'pwd'
          sh 'docker build -t $CALCULATION_SERVICE_IMAGE:latest -t $CALCULATION_SERVICE_IMAGE:$BUILD_NUMBER .'
          sh 'docker tag $CALCULATION_SERVICE_IMAGE:latest $ECR_ID/$CALCULATION_SERVICE_IMAGE:latest'
          sh 'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID'
          sh 'docker image prune -f'
          sh 'docker push $ECR_ID/$CALCULATION_SERVICE_IMAGE:latest'
          sh 'docker logout'
        }

      }
    }

    stage('Prepare Validation Response Daemon') {
      steps {
        dir(path: 'source/creditcard-identity-verification-response-daemon') {
          sh 'docker build -t $VALIDATION_RESPONSE_DAEMON_IMAGE:latest -t $VALIDATION_RESPONSE_DAEMON_IMAGE:$BUILD_NUMBER .'
          sh 'docker tag $VALIDATION_RESPONSE_DAEMON_IMAGE:latest $ECR_ID/$VALIDATION_RESPONSE_DAEMON_IMAGE:latest'
          sh 'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID'
          sh 'docker image prune -f'
          sh 'docker push $ECR_ID/$VALIDATION_RESPONSE_DAEMON_IMAGE:latest'
          sh 'docker logout'
        }

      }
    }

    stage('Prepare Credit Card Service') {
      steps {
        dir(path: 'source/creditcard-service') {
          sh 'pwd'
          sh 'docker build -t $CREDITCARD_SERVICE_IMAGE:latest -t $CREDITCARD_SERVICE_IMAGE:$BUILD_NUMBER .'
          sh 'docker tag $CREDITCARD_SERVICE_IMAGE:latest $ECR_ID/$CREDITCARD_SERVICE_IMAGE:latest'
          sh 'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID'
          sh 'docker image prune -f'
          sh 'docker push $ECR_ID/$CREDITCARD_SERVICE_IMAGE:latest'
          sh 'docker logout'
        }

      }
    }

    stage('Prepare Email Service') {
      steps {
        dir(path: 'source/email-service') {
          sh 'pwd'
          sh 'docker build -t $EMAIL_SERVICE_IMAGE:latest -t $EMAIL_SERVICE_IMAGE:$BUILD_NUMBER .'
          sh 'docker tag $EMAIL_SERVICE_IMAGE:latest $ECR_ID/$EMAIL_SERVICE_IMAGE:latest'
          sh 'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID'
          sh 'docker image prune -f'
          sh 'docker push $ECR_ID/$EMAIL_SERVICE_IMAGE:latest'
          sh 'docker logout'
        }

      }
    }

    stage('Prepare Identity Verification Service') {
      steps {
        dir(path: 'source/identity-verification-service') {
          sh 'pwd'
          sh 'docker build -t $IDENTITY_VERIFICATION_SERVICE_IMAGE:latest -t $IDENTITY_VERIFICATION_SERVICE_IMAGE:$BUILD_NUMBER .'
          sh 'docker tag $IDENTITY_VERIFICATION_SERVICE_IMAGE:latest $ECR_ID/$IDENTITY_VERIFICATION_SERVICE_IMAGE:latest'
          sh 'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID'
          sh 'docker image prune -f'
          sh 'docker push $ECR_ID/$IDENTITY_VERIFICATION_SERVICE_IMAGE:latest'
          sh 'docker logout'
        }

      }
    }

  }
  environment {
    ECR_ID = '142198642907.dkr.ecr.us-west-1.amazonaws.com'
    CALCULATION_SERVICE_IMAGE = 'gaurav2-casestudy-calculation-service'
    ECR_CREDENTIALS = credentials('ecr-credentials')
    VALIDATION_RESPONSE_DAEMON_IMAGE = 'gauravv2-casestudy-creditcard-identity-verification-response-daemon'
    EMAIL_SERVICE_IMAGE = 'gauravv2-casestudy-email-service'
    CREDITCARD_SERVICE_IMAGE = 'gauravv2-casestudy-creditcard-service'
    IDENTITY_VERIFICATION_SERVICE_IMAGE = 'gauravv2-casestudy-identity-verification-service'
  }
}