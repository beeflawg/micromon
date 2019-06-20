node {
    def app

    stage("Clone repository"){
        /* clone the repository*/
        checkout scm
    }

    stage("Permissions"){
       
           stage("AdminServer"){
                /* change directory */
                dir("AdminServer"){
                /* set maven wrapper permission */
                sh "chmod 711 ./mvnw"
                }
           }
           stage("DiscoveryServer"){
                /* change directory */
                dir("DiscoveryServer"){
                /* set maven wrapper permission */
                sh "chmod 711 ./mvnw"
                }
           }
       
    }

    stage("Test"){
        /* change directory */
        dir("AdminServer"){
        /* run test */
        sh "./mvnw test"
        }
    }

    stage("Build Project"){
        /* change directory */
        dir("AdminServer"){
        /* build the project */
        sh "./mvnw clean install"
        }
    }

    stage ("Build Image"){
        /* change directory */
        dir("AdminServer"){
        app = docker.build("beeflawg/admin-server")
        }
    }

    stage ("Push Image"){
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