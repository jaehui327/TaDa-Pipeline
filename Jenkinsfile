pipeline {
    agent any
    environment {
        imagename = "tada-back"
    }
    stages {
        stage('Clone Repository') {
            steps {
                echo "Clonning Repository"
                git url: 'https://lab.ssafy.com/s08-final/S08P31A503.git',
                branch: 'dev-back',
                 credentialsId: 'jaeheekim970327'
            }
            post {
                success {
                    echo 'Successfully Cloned Repository'
                }
                failure {
                    error 'This pipeline stops here...'
                }
            }
        }
        stage('Build Gradle') {
            steps {
                echo 'Build Gradle'
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
            post {
                failure {
                    error 'This pipeline stops here...'
                }
            }
        }
        stage('Build Docker') {
            steps {
                echo 'Build Docker'
                script {
                    dockerImage = docker.build imagename
                }
            }
            post {
                failure {
                    error 'This pipeline stops here...'
                }
            }
        } 
    }
}

