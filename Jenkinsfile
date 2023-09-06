@Library('shared-library') _

pipeline{

    agent any

    parameters{
        string(name: 'appName', description: 'Name by which API will be deployed', defaultValue: 'jenkins-demo-pratik-api')
        string(name: 'deployEnv', description: 'Env Name where API will get deployed', defaultValue: 'Sandbox')
        string(name: 'region', description: 'Region where API will get deployed', defaultValue: 'us-east-1')
        string(name: 'workers', description: 'No of workers', defaultValue: '1') 
        string(name: 'workerType', description: 'Type of worker', defaultValue: 'MICRO')
        string(name: 'platformClientId', description: 'Anypoint Platform Client Id')
        string(name: 'platformClientSecret', description: 'Anypoint Platform Client Secret')
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