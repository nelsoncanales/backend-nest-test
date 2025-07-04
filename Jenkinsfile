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
                stage("ejecucion de pruebas"){
                    steps {
                        sh 'npm run test:cov'
                    }
                }
                stage("construccion de la aplicacion"){
                    steps {
                        sh 'npm run build'
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