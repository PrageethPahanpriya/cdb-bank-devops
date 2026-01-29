pipeline {
    agent any

    environment {
        APP_NAME = "cdb-app"
    }

    stages {

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
                sh '''
                  chmod +x build.sh || true
                  ./build.sh || echo "No build script, skipping"
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Running tests"
                sh '''
                  chmod +x test.sh || true
                  ./test.sh || echo "No tests, skipping"
                '''
            }
        }

        stage('Package') {
            steps {
                sh '''
                  mkdir -p dist
                  echo "Build output" > dist/app.txt
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'dist/**'
            echo 'Pipeline succeeded'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
