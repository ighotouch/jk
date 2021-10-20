pipeline {
    agent {
        kubernetes {
            yamlFile 'build-pod.yaml'
            defaultContainer 'default'
        }
    }
    stages {
        stage('terraform init'){
            steps {
                echo 'Hellow world'
            }
        }
    }
}
