pipeline {
    agent any

    parameters {
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Select the action to perform')
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws_access_key')
        AWS_SECRET_ACCESS_KEY = credentials('aws_secret_key')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Terraform code from Git
                git 'https://github.com/nishantddubey/terraform_pipeline_repo.git'
            }
        }
            stage('Apply / Destroy') {
            steps {
                script {
                    if (params.action == 'apply') {

                        sh 'terraform init && terraform plan && terraform apply --auto-approve'

                    } else if (params.action == 'destroy') {
                        sh 'terraform init terraform plan && terraform destroy --auto-approve'
                    } else {
                        error "Invalid action selected. Please choose either 'apply' or 'destroy'."
                    }
                }
            
            }
        }
    }
}

