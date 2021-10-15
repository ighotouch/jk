pipeline {
    agent {
        kubernetes {
            yamlFile 'build-pod.yaml'
            defaultContainer 'myapp'
        }
    }
    stages {
        stage('terraform init'){
            steps {
                sh "ls"
            }
        }
    }
}
