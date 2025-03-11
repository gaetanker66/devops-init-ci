pipeline {
    agent any

    environment {
        NODE_VERSION = "22.x"
    }

    stages {
        stage('Setup Node.js') {
            steps {
                script {
                    def nodeHome = tool name: "nodejs-${NODE_VERSION}", type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${nodeHome}/bin:${env.PATH}"
                }
            }
        }
        stage('Install dependencies') {
            steps {
                echo 'Installation des dépendances...'
                sh 'npm install'
            }
        }
        stage('Run tests') {
            steps {
                echo 'Exécution des tests...'
                sh 'npm test'
            }
        }
    }
    post {
        always {
            echo 'Nettoyage post-build...'
            sh 'rm -rf node_modules'
        }
    }
}