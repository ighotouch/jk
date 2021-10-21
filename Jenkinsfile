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
                withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) {
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
