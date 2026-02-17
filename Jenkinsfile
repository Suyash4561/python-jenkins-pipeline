stage('Setup Python Environment') {
    steps {
        echo 'Setting up Python environment...'
        // Create virtual environment
        bat 'python -m venv venv'
        // Activate venv and upgrade pip
        bat '.\\venv\\Scripts\\activate && python -m pip install --upgrade pip'
        // Install dependencies
        bat '.\\venv\\Scripts\\activate && python -m pip install -r requirements.txt'
    }
}

stage('Run Tests') {
    steps {
        echo 'Running pytest...'
        bat '.\\venv\\Scripts\\activate && python -m pytest test_app.py --junitxml=test-reports/results.xml --html=test-reports/report.html --self-contained-html'
    }
}
