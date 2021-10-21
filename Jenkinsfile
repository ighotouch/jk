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
                    sh '''
                        terraform init
                        terraform plan --out tfplan.binary
                        terraform show -json tfplan.binary > tfplan.json
                    '''
                 }
            }
        }
        stage('OPA'){
            agent {
                kubernetes {
                    yamlFile 'build-pod.yaml'
                    defaultContainer 'opa'
                }
            }
            steps {
                sh '''
                    opa eval --format pretty --data terraform.rego --input tfplan.json "data.terraform.analysis.authz"
                '''
            }
        }
    }
}
