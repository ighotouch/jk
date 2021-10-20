pipeline {
    agent {
        kubernetes {
            yamlFile 'build-pod.yaml'
            defaultContainer 'jenkins'
        }
    }
    stages {
        stage('terraform init'){
            steps {
                terraform show
            }
        }
    }
}
