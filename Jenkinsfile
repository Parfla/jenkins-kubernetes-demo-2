pipeline {
    agent any
    environment {
        leenewcredentials = credentials('leenewcredentials')
    }
    stages {
        stage('Create Secret') {
            steps {
                sh "sed -e 's,{{SECRET_KEY}},'${leenewcredentials}',g;' credentials.yaml | kubectl apply -f -"
            }
        }
        stage('Deploy App') {
            steps {
                sh "kubectl apply -f todo.yaml"
                sh "sleep 50"
                sh "kubectl get svc todo"
            }
        }
    }
}