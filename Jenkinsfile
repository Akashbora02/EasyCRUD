pipeline{
    agent{
        label 'webserver'
    }
    stages{
        stage('Pull'){
            steps{
                git branch: 'main', credentialsId: 'acedaee5-0bf0-410e-89c5-46cc66ba198d', url: 'https://github.com/Akashbora02/EasyCRUD.git'
            }
        }
        stage('Build'){
            steps{
                    sh '''
                    sudo chmod +x docker-install.sh
                    ./docker-install.sh
                    '''
            }
        }
        stage('Test'){
            steps{
                sh '''
                sonar-scanner \
              -Dsonar.projectKey=EASYCRUD \
              -Dsonar.sources=. \
              -Dsonar.host.url=http://18.212.184.129:9000 \
              -Dsonar.login=sqp_d4170d3ee44d4d5dfe746d1ad37fbf15972d1a16
                '''
            }
        }
    }
}