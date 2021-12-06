pipeline {
  agent any
  stages {
    stage('Prepare calculation-offer-service') {
      steps {
        dir(path: 'source/calculation-offer-service/CalculationServiceAPISolution') {
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

  }
  environment {
    ECR_ID = '142198642907.dkr.ecr.us-west-1.amazonaws.com'
    CALCULATION_SERVICE_IMAGE = 'gaurav2-casestudy-calculation-service'
    ECR_CREDENTIALS = credentials('ecr-credentials')
  }
}