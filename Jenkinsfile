pipeline{
    agent{
        label 'webserver'
    }
    tools {
        nodejs 'node18'
        sonarScanner 'sonar-scanner'
    }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', credentialsId: 'acedaee5-0bf0-410e-89c5-46cc66ba198d', url: 'https://github.com/Akashbora02/EasyCRUD.git'
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