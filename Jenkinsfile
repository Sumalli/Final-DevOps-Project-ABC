pipeline {
    agent any
    tools {
        maven 'Apache-Maven'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], 
                userRemoteConfigs: [[url: 'https://github.com/Sumalli/Final-DevOps-Project-ABC.git']])
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
 
        stage('Unit Testing') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
 
        stage('Package') {
            steps {
                sh 'mvn package'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }

        stage('Clean and Install') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}

