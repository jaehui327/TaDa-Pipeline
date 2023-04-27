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
                 credentialsId: '95086913-a1b2-4c08-8a34-382f19454773'
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
                dir ('/backend/tada') {
                    sh 'chmod +x gradlew'
                    sh './gradlew clean --debug build'
                }
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

