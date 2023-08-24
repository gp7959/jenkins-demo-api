@Library('shared-Library') _

pipeline{

    agent any

    stages{
        stage('Git Checkout'){
            steps{

                script{
                    gitCheckout(
                        branch: "develop"
                        url: "https://github.com/gp7959/jenkins-demo-api.git"
                    )
                }
            }
        }
    }
}