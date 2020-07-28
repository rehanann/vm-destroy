pipeline {
  agent any
  environment {
    SVC_ACCOUNT_KEY = credentials('terraform-auth')
    VARIABLES = credentials('VARIABLES')
    PROVIDER = credentials('PROVIDER')
  }
  stages {
            stage('Checkout') {
                steps {
                    checkout scm
                    sh 'echo $SVC_ACCOUNT_KEY | base64 -d > serviceaccount.json'
                    sh 'echo $PROVIDER | base64 -d > provider.tf'
                    sh 'echo $VARIABLES | base64 -d > variable.tf'
                    }
             }
        stage('TF Apply') {
                steps {
                    sh 'terraform init'
                    sh 'terraform destroy -auto-approve '
            }
        }
    }
}