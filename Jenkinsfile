@Library('shared-library') _

pipeline{

    agent any

    stages{
        stage('Git Checkout'){
            steps{
                script{
                    gitCheckout(
                        branch: "develop",
                        url: "https://github.com/gp7959/jenkins-demo-api.git",
                        credentialsId: "GITHUBCREDS"
                    )
                }
            }
        }

        stage('Munit Testing'){
            tools {
                   jdk "JAVA_HOME"
                }
            steps{
                script{
                    munitTest()
                }
            }
        }

        stage('SonarQube Scan'){
            tools {
                   jdk "JAVA_HOME_17"
                }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'SONARTOKEN')
                    sonarScan()
                }
            }
        }

        stage('Build Jar'){
            steps{
                script{
                    buildJar()
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

        stage('Deploy to CloudHub'){
            steps{
                script{
                    deployToCloudhub()
                }
            }
        }
    }
}