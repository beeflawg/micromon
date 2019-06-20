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
        /* run test */
        sh "./mvnw test"
    }

    stage("Build Project"){
        /* build the project */
        sh "./mvnw clean install"
    }

    stage ("Build Image"){
        app = docker.build("beeflawg/admin-server")
    }

    stage ("Push Image"){
        /* push the image to docker hub */
        sh "echo TODO"
    }

}