node {
    def app

    stage("Clone repository"){
        /* clone the repository*/
        checkout scm
    }

    stage("Permissions"){
        /* change directory */
        dir("AdminServer"){
        /* set maven wrapper permission */
        sh "chmod 711 ./mvnw"
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
        sh "echo TODO"
        }
    }

}