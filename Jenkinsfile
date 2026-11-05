pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Fetching project files'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Student Portfolio'

                bat '''
                    if not exist dist mkdir dist
                    copy /Y index.html dist\\index.html
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing website'

                bat '''
                    if not exist index.html exit /b 1
                    findstr /i /c:"Student Portfolio" index.html
                    if errorlevel 1 exit /b 1
                    echo All tests passed!
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'dist/**'
            }
        }
    }

    post {
        success {
            echo 'PROJECT BUILD SUCCESSFUL!'
        }

        failure {
            echo 'PROJECT BUILD FAILED!'
        }
    }
}
