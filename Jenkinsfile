@Library('shared-library') _

pipeline{

    agent any

    parameters{
        string(name: 'appName', description: 'Name by which API will be deployed', defaultValue: 'jenkins-demo-pratik-api')
        string(name: 'deployEnv', description: 'Env Name where API will get deployed', defaultValue: 'Sandbox')
        string(name: 'region', description: 'Region where API will get deployed', defaultValue: 'us-east-1')
        string(name: 'workers', description: 'No of workers', defaultValue: '1') 
        string(name: 'workerType', description: 'Type of worker', defaultValue: 'MICRO')
        string(name: 'platformClientId', description: 'Anypoint Platform Client Id', defaultValue: 'a79b0e9313a245de8c41ffd2b1afe09e')
        string(name: 'platformClientSecret', description: 'Anypoint Platform Client Secret', defaultValue: '69F8F7fEB2Cd422f9CA8e66bEe60d5DF')
    }

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
                    def credId = "SONARTOKEN"
                    sonarScan(credId)
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
                    deployToCloudhub(
                        appName: "${params.appName}",
                        deployEnv: "${params.}",
                        region: "${params.region}",
                        workers: "${params.workers}",
                        workerType: "${params.workerType}",
                        platformClientId: "${params.platformClientId}",
                        platformClientSecret: "${params.platformClientSecret}"
                    )
                }
            }
        }
    }
}