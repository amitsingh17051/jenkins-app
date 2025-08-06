pipeline {
    agent {
        docker {
            image 'node:24'
            args '-u root:root' // avoid npm permission issues
        }
    }

    stages {
        stage('Check Versions') {
            steps {
                sh 'node -v'
                sh 'npm -v'
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
    }

    post {
        always {
            echo 'Build complete.'
        }
    }
}
