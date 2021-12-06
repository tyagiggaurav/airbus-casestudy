pipeline {
  agent any
  stages {
    stage('Prepare calculation-offer-service') {
      steps {
        dir(path: 'source/calculation-offer-service/CalculationServiceAPISolution') {
          sh ' sh \'pwd\''
          sh 'sh \'docker build -t $CALCULATION_SERVICE_IMAGE:latest -t $CALCULATION_SERVICE_IMAGE:$BUILD_NUMBER .\''
          sh 'sh \'docker tag $CALCULATION_SERVICE_IMAGE:latest $ECR_ID/$CALCULATION_SERVICE_IMAGE:latest\''
          sh ' sh \'docker tag $CALCULATION_SERVICE_IMAGE:$BUILD_NUMBER $ECR_ID/$CALCULATION_SERVICE_IMAGE:$BUILD_NUMBER\''
          sh ' sh \'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID\''
          sh ' sh \'docker image prune -f\''
          sh ' sh \'docker push $ECR_ID/$CALCULATION_SERVICE_IMAGE:latest\''
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