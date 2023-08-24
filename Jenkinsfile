pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{

                script{

                    git branch: 'develop', url: 'https://github.com/gp7959/jenkins-demo-api.git'
                }
            }
        }
    }
}