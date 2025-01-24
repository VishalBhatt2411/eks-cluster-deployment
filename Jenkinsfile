pipeline {
    agent any
environment {
    AWS_ACCESS_KEY_ID = credentials('AKIAUQ4L3NZQHDNZOI6D')
    AWS_SECRET_ACCESS_KEY = credentials('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')
  }
    parameters {
        choice(
            name: 'ACTION',
            choices: ['apply', 'destroy'],
            description: 'Select the action to perform'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/VishalBhatt2411/eks-cluster-deployment.git'
            }
        }
    
        stage ("terraform init") {
            steps {
                sh ("terraform init -reconfigure") 
            }
        }
        
        stage ("plan") {
            steps {
                sh ('terraform plan') 
            }
        }

        stage (" Action") {
            steps {
                script {
                    switch (params.ACTION) {
                        case 'apply':
                            echo 'Executing Apply...'
                            sh "terraform apply --auto-approve"
                            break
                        case 'destroy':
                            echo 'Executing Destroy...'
                            sh "terraform destroy --auto-approve"
                            break
                        default:
                            error 'Unknown action'
                    }
                }
            }
        }
    }
}
