pipeline{
    agent{
        label 'webserver'
    }
    tools {
        nodejs 'node18'
    }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', credentialsId: '8b6c1da2-3b18-4f7c-b4f5-ef9111c139a0', url: 'https://github.com/Akashbora02/EasyCRUD.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                  echo "Installing npm dependencies..."
                  npm install
                '''
            }
        }
        stage('Build'){
            steps{
                    sh '''
                    echo "Building Docker image..."
                    docker build -t easycrud:latest .
                    '''
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('sonar-token')
                }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                    pwd
                    ls
                    sonar-scanner \
                    -Dsonar.projectKey=EASYCRUD \
                    -Dsonar.sources=. \
                    -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                echo "Deploying Docker container..."

                # Stop and remove old container if exists
                docker stop easycrud || true
                docker rm easycrud || true

                # Run new container
                docker run -d \
                --name easycrud \
                -p 3000:80 \
                easycrud:latest
                '''
            }
        }
    }
}