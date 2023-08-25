@Library('shared-library') _

pipeline{

    agent any

    stages{
        stage('Git Checkout'){
            steps{

                script{
                    gitCheckout(
                        branch: "develop",
                        url: "https://github.com/gp7959/jenkins-demo-api.git"
                    )
                }
            }
        }

        stage('Munit Test'){
            steps{
                script{
                    munitTest()
                }
            }
        }

        stage('Push to Nexus'){
            steps{
                script{
                    nexusPush()
                }
            }
        }
    }
}