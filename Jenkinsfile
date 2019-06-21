pipeline {
    agent any
    
    stages{
        stage("Clone repository"){
            steps{
                /* clone the repository*/
                checkout scm
            }
        }

        stage("Permissions"){
            parallel{
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
                stage("Pokemon Service"){
                    steps{
                        /* change directory */
                        dir("PokemonService"){
                        /* set maven wrapper permission */
                        sh "chmod 711 ./mvnw"
                        }
                    }
                }
                stage("Trainer Service"){
                    steps{
                        /* change directory */
                        dir("TrainerService"){
                        /* set maven wrapper permission */
                        sh "chmod 711 ./mvnw"
                        }
                    }
                }
            }
        }

        stage("Test"){
            parallel{
                stage("Admin Test"){
                    steps{
                        /* change directory */
                        dir("AdminServer"){
                        /* run test */
                        sh "./mvnw test"
                        }
                    }
                }
                stage("Discovery Test"){
                    steps{
                        /* change directory */
                        dir("DiscoveryServer"){
                        /* run test */
                        sh "./mvnw test"
                        }
                    }
                }
                stage("Pokemon Test"){
                    steps{
                        /* change directory */
                        dir("PokemonService"){
                        /* run test */
                        sh "./mvnw test"
                        }
                    }
                }
                stage("Trainer Test"){
                    steps{
                        /* change directory */
                        dir("TrainerService"){
                        /* run test */
                        sh "./mvnw test"
                        }
                    }
                }
            }
        }

        stage("Build Project"){
            parallel{
                stage("Build Admin"){
                    steps{
                        /* change directory */
                        dir("AdminServer"){
                        /* build the project */
                        sh "./mvnw clean install"
                        }
                    }
                }
                stage("Build Discovery"){
                    steps{
                        /* change directory */
                        dir("DiscoveryServer"){
                        /* build the project */
                        sh "./mvnw clean install"
                        }
                    }
                } 
                stage("Build Pokemon"){
                    steps{
                        /* change directory */
                        dir("PokemonService"){
                        /* build the project */
                        sh "./mvnw clean install"
                        }
                    }
                } 
                stage("Build Trainer"){
                    steps{
                        /* change directory */
                        dir("TrainerService"){
                        /* build the project */
                        sh "./mvnw clean install"
                        }
                    }
                }   
            }
        }

        stage ("Build Image"){
            parallel{
                stage("Build AS Image"){
                    steps{  
                        /* change directory */
                        dir("AdminServer"){
                            script{
                                app = docker.build("beeflawg/admin-server")
                            }
                        }     
                    }
                }
                stage("Build DS Image"){
                    steps{  
                        /* change directory */
                        dir("DiscoveryServer"){
                            script{
                                app2 = docker.build("beeflawg/discovery-server")
                            }
                        }     
                    }
                }
                stage("Build PS Image"){
                    steps{  
                        /* change directory */
                        dir("PokemonService"){
                            script{
                                app3 = docker.build("beeflawg/pokemon-service")
                            }
                        }     
                    }
                }
                stage("Build TS Image"){
                    steps{  
                        /* change directory */
                        dir("TrainerService"){
                            script{
                                app4 = docker.build("beeflawg/trainer-service")
                            }
                        }     
                    }
                }
            }
        }

        stage ("Push Image"){
            parallel{
                stage("Push Admin Server"){
                    steps{
                        /* change directory */
                        dir("AdminServer"){
                        /* push the image to docker hub */
                            script{
                                docker.withRegistry("https://registry.hub.docker.com", "docker-hub-credentials"){
                                    app.push("${env.BUILD_NUMBER}")
                                    app.push("latest")
                                }
                            }
                        }
                    }
                }
                stage("Push Admin Server"){
                    steps{
                        /* change directory */
                        dir("DiscoveryServer"){
                        /* push the image to docker hub */
                            script{
                                docker.withRegistry("https://registry.hub.docker.com", "docker-hub-credentials"){
                                    app2.push("${env.BUILD_NUMBER}")
                                    app2.push("latest")
                                }
                            }
                        }
                    }
                }
                stage("Push Pokemon Service"){
                    steps{
                        /* change directory */
                        dir("PokemonService"){
                        /* push the image to docker hub */
                            script{
                                docker.withRegistry("https://registry.hub.docker.com", "docker-hub-credentials"){
                                    app3.push("${env.BUILD_NUMBER}")
                                    app3.push("latest")
                                }
                            }
                        }
                    }
                }
                stage("Push Trainer Service"){
                    steps{
                        /* change directory */
                        dir("TrainerService"){
                        /* push the image to docker hub */
                            script{
                                docker.withRegistry("https://registry.hub.docker.com", "docker-hub-credentials"){
                                    app4.push("${env.BUILD_NUMBER}")
                                    app4.push("latest")
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}