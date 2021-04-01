pipeline{
    agent any

    stages{
        stage('Checkout Source'){
            steps{
                git url: 'https://github.com/DaianCosta/pedelogo-catalogo'
            }
        }

        stage('Build Image'){
            steps{
                script{
                    dockerapp = docker.build("desenvolvimentodaian/api-produto:${env.BUILD_ID}",
                    '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')    
                }
            }
        }

        stage('Push Image'){
            steps{
                script{
                        docker.withRegistry('https://registry.hub.docker.com','dockerhub'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")  
                    }
                }
            }
        }
    }
}