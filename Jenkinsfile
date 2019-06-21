pipeline {
    agent any
    node{
    def app

    stages{
        stage("Clone repository"){
            steps{
                /* clone the repository*/
                checkout scm
            }
        }

        stage("Permissions"){
            stages{
                stage("Admin Server"){
                    steps{
                        /* change directory */
                        dir("AdminServer"){
                        /* set maven wrapper permission */
                        sh "chmod 711 ./mvnw"
                        }
                    }
                }
                stage("Discovery Server"){
                    steps{
                        /* change directory */
                        dir("DiscoveryServer"){
                        /* set maven wrapper permission */
                        sh "chmod 711 ./mvnw"
                        }
                    }
                }
            }
        }

        stage("Test"){
            steps{
                /* change directory */
                dir("AdminServer"){
                /* run test */
                sh "./mvnw test"
                }
            }
        }

        stage("Build Project"){
            steps{
                /* change directory */
                dir("AdminServer"){
                /* build the project */
                sh "./mvnw clean install"
                }
            }
        }

        stage ("Build Image"){
            steps{
                /* change directory */
                dir("AdminServer"){
                app = docker.build("beeflawg/admin-server")
                }
            }
        }

        stage ("Push Image"){
            steps{
                /* change directory */
                dir("AdminServer"){
                /* push the image to docker hub */
                    docker.withRegistry("https://registry.hub.docker.com", "docker-hub-credentials"){
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
    }
}