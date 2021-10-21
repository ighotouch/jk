pipeline {
    agent {
        kubernetes {
            yamlFile 'build-pod.yaml'
            defaultContainer 'terraform'
        }
    }
    stages {
        stage('terraform init'){
            steps { 
                withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'igho-aws-creds', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    script {
                        sh 'aws ec2 describe-instances'
                        sh 'terraform init'
                        sh 'opa eval --format pretty --data terraform.rego --input tfplan.json "data.terraform.analysis.authz"'
                    }
                }
            }
        }
    }
}
