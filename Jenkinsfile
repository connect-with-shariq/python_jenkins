pipeline {
    agent any
    
    environment {
        PYTHON_VERSION = '3.9'
    }
    

    
    stages {
        
        stage('Setup Python') {
            steps {
                echo "Setting up Python environment..."
                sh 'python3 --version'
                sh 'pip3 --version'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo "Installing Python dependencies..."
                sh 'pip3 install -r requirements.txt'
            }
        }
        
        
        stage('Run Application') {
            steps {
                echo "Running the application..."
                sh 'python3 app.py'
            }
        }
        
        stage('Run Tests') {
            steps {
                echo "Running unit tests..."
                sh 'python3 -m pytest test_app.py -v --tb=short'
            }
        }
        
        stage('Test Coverage') {
            steps {
                echo "Generating test coverage report..."
                sh 'python3 -m pytest test_app.py --cov=app --cov-report=term-missing || true'
            }
        }
        
        stage('Build Artifacts') {
            steps {
                echo "Creating build artifacts..."
                sh '''
                    mkdir -p dist
                    cp app.py dist/
                    cp test_app.py dist/
                    cp requirements.txt dist/
                    echo "Artifacts ready in dist/ directory"
                '''
            }
        }
    }
    
    post {
        always {
            echo "Cleaning up workspace..."
            cleanWs()
        }
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed! Check logs above."
        }
    }
}
