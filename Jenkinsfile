pipeline{
    agent any
    environment {
        DOCKER_IMAGE="chaithracs/app"
    
    }
    stages{
        stage('clone Repository'){
            steps{
                git 'https://github.com/chaithracs/https://github.com/chaithracs944-ops/docker.git'

            
            }
        
        }
    
    }
    stage('Build Docker Image'){
        steps{
            script{
                docker.build("${DOCKER_IMAGE}:latest")
            }
        }
    }
    stage('Login to Docker Hub'){
        steps{
            withCredentials([usernamePassword(
                credentialsId: 'dockerhub-creds1',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS'

            )]){
                bat 'echo $DOCKER_PASS | docker login -u $chaithracs --password-stdin'

            }
        }
    }
    stage('Push Docker Image'){
                steps{
                    script{
                        docker.withRegistry('','dockerhub-creds1'){
                            docker.image("${DOCKER_IMAGE}:latest").push()
                        }
                
                    }
                }

            }

    post{
        success{
            echo 'Image successfully built and pushed to Docker Hub'
        }
        failure{
            echo 'Pipeline failed'
        }
    }

}