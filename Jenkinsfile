pipeline {
    agent any // This will run the pipeline on any available agent

    stages {
        stage('Clone Repo') {
            steps {
                script {
                    def WORKSPACE = "/Spring_boot_project/spring-mysql/spring-mysql"
                    def dockerImageTag = "spring-mysql${env.BUILD_NUMBER}"

                    try {
                        git url: 'https://github.com/gituserpr707/docker-spring-boot.git',
                            credentialsId: 'gituserpr707',
                            branch: 'main'
                    } catch (Exception e) {
                        throw e
                    }
                }
            }
        }

        stage('Build docker') {
            steps {
                script {
                    dockerImage = docker.build("spring-mysql:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Deploy docker') {
            steps {
                script {
                    echo "Docker Image Tag Name: ${dockerImageTag}"
                    bat "docker stop spring-mysql || true && docker rm spring-mysql || true"
                    bat "docker run --name spring-mysql -d -p 8081:8081 spring-mysql:${env.BUILD_NUMBER}"
                }
            }
        }
    }
}