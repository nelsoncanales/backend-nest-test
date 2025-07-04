pipeline {
    agent any

    environment{
        NPM_CONFIG_CACHE= "${WORKSPACE}/.npm"
        dockerImagePrefix = "us-west1-docker.pkg.dev/lab-agibiz/docker-repository"
        registry = "https://us-west1-docker.pkg.dev"
        registryCredentials = 'gcp-registrynco'
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

        stage ("DOCKER"){
            steps {
                script {
                    docker.withRegistry("${registry}", registryCredentials ){
                        sh "docker build -t backend-nest-test-ncanales ."
                        sh "docker tag backend-nest-test-ncanales ${dockerImagePrefix}/backend-nest-test-ncanales:${BUILD_NUMBER}"
                        sh "docker push ${dockerImagePrefix}/backend-nest-test-ncanales:${BUILD_NUMBER}"
                        sh "docker tag backend-nest-test-ncanales ${dockerImagePrefix}/backend-nest-test-ncanales"
                        sh "docker push ${dockerImagePrefix}/backend-nest-test-ncanales"
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