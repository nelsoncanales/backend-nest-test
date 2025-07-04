pipeline {
    agent any

    stages{
        stage ("Paso 1 del stage Tarea Final") {
            steps {
                sh 'echo "comenzado pipeline Ultima Tarea"'
            }
        }

        stage ("proceso de build y test") {
            agent {
                docker {
                    image 'node:22'
                    reuseNode true
                }
            }
            stages {
                stage("instalacion de dependencias"){
                    steps {
                        sh 'npm ci'
                    }
                }
            }
        }

        stage ("Paso 2 ") {
            steps {
                sh 'echo "Paso Final del stage Tarea Final"'
            }
        }
    }
}