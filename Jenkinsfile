pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/MasDiptha12/sast-demo-app.git', branch: 'master'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Create virtual environment
                    sh 'python3 -m venv venv'
                    // Activate the virtual environment and install bandit
                    sh '. venv/bin/activate && pip install bandit'
                }
            }
        }
        stage('SAST Analysis') {
            steps {
                // Run bandit analysis
                sh '. venv/bin/activate && bandit -f xml -o bandit-output.xml -r . || true'
                // Record issues
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}
