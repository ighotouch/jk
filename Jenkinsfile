pipeline {
    agent {
        kubernetes {
            yamlFile 'build-pod.yaml'
            defaultContainer 'static-web'
        }
    }
    stages {
        stage('terraform init'){
            steps {
                script {
                    sh 'terraform init'
                    sh 'opa eval --format pretty --data terraform.rego --input tfplan.json "data.terraform.analysis.authz"'
                }
            }
        }
    }
}
