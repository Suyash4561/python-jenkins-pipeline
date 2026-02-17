pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                git branch: 'main', url: 'https://github.com/Suyash4561/python-jenkins-pipeline.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                echo 'Creating Python virtual environment...'
                bat 'python -m venv venv'
                bat '.\\venv\\Scripts\\activate && python -m pip install --upgrade pip'
                bat '.\\venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo 'Running tests...'
                bat '.\\venv\\Scripts\\activate && pytest test_app.py --junitxml=test-reports/results.xml --html=test-reports/report.html --self-contained-html'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                    publishHTML(target: [
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'test-reports',
                        reportFiles: 'report.html',
                        reportName: 'Pytest HTML Report'
                    ])
                }
            }
        }
    }

    post {
        success {
            echo 'Python CI Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check test reports!'
        }
    }
}
