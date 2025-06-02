pipeline {
    agent { label 'KMaster' }

    parameters {
        string(name: 'BUILD_TAG', defaultValue: 'latest', description: 'Tag of Docker Image')
    }

    stages {
        stage('Cloning Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Rakshitsen/Cd-pipeline.git'
            }
        }



        stage('Deploy to K8s') {
            steps {
                sh "sed -i 's|tag|${params.BUILD_TAG}|' deployment.yaml"
                sh "kubectl apply -f deployment.yaml --validate=false"
                sh "kubectl apply -f service.yaml"
                sh "kubectl get service"
            }
        }
    }
}
