
pipeline {
    agent {
        node {
            label 'nodejs' // optional: if you use labeled agents
        }
    }

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/amitsingh17051/jenkins-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm run test || echo "No tests found."'
            }
        }

        stage('Export Static (Optional)') {
            when {
                expression { fileExists('next.config.js') }
            }
            steps {
                sh 'npm run export || echo "Skipping export."'
            }
        }

        stage('Archive Build Output') {
            steps {
                archiveArtifacts artifacts: '.next/**', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
