pipeline {
    agent any
    tools {
            jdk 'jdk21'
            maven 'maven'
    }
    environment {
            REPO_URL = 'git remote add origin https://github.com/aedrif/TPGestionBib.git'
            SONARQUBE_CREDENTIALS_ID = 'sonar'
    }
    stages {
         stage('clean work-space') {
                    steps {
                        cleanWs()
                    }
         }
         stage('Checkout from github') {
                     steps {
                         git branch: 'main',
                         credentialsId: '9da44a34-3ff6-4fd2-986d-d0f2adedc6dd',
                         url: REPO_URL
                     }
         }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Quality Analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonar' , credentialsId: SONARQUBE_CREDENTIALS_ID) {
                                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Déploiement simulé réussi'
            }
        }
    }
     post {
            success {
                mail(
                    to: 'edrifayoub36@gmail.com',
                    subject: 'Build Success',
                    body: 'Le build a été complété avec succès.'
                )
            }
            failure {
                mail(
                    to: 'edrifayoub36@gmail.com',
                    subject: 'Build Failed',
                    body: 'Le build a échoué.'
                )
            }
     }
}
