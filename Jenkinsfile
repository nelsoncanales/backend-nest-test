pipeline {
    agent any

    environment{
        NPM_CONFIG_CACHE= "${WORKSPACE}/.npm"
    }

    stages{
        stage ("Paso 1 del stage Tarea Final") {
            steps {
                sh 'echo "comenzado pipeline Ultima Tarea"'
            }
        }

        stage ("Paso 2 Tarea Final Instalar, probar y construir") {
            agent {
                docker {
                    image 'node:22'
                    reuseNode true
                }
            }
            stages {
                stage("dependencias"){
                    steps {
                        sh 'npm ci'
                    }
                }            
                stage("Test"){
                steps {
                        sh 'npm run test:cov'
                    }
                }
                stage("construir"){
                steps {
                        sh 'npm run build'
                    }
                }
            }
        }

        stage ("Paso Final ") {
            steps {
                sh 'echo "Paso Final del stage N Tarea Final"'
            }
        }

    }

}