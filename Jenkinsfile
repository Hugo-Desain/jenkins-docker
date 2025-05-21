pipeline {
    agent any

    environment {
        IMAGE_NAME = 'monsite-docker'
        CONTAINER_NAME = 'monsite-docker-conteneur'
    }

    stages {
        stage('Vérifier les fichiers') {
            steps {
                script {
                    if (!fileExists('Dockerfile') || !fileExists('index.html')) {
                        error('Dockerfile ou index.html manquant !')
                    }
                }
            }
        }

        stage('Construire l’image Docker') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Supprimer ancien conteneur') {
            steps {
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }

        stage('Lancer le conteneur') {
            steps {
                sh "docker run -d --name ${CONTAINER_NAME} -p 8081:80 ${IMAGE_NAME}"
            }
        }
    }
}
