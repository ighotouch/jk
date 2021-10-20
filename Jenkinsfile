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
                script {
                    sh 'terraform init'
                    sh 'terraform plan --out tfplan.binary'
                    sh 'terraform show -json tfplan.binary > tfplan.json'
                }
            }
        }
    }
}
