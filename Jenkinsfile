pipeline {
    agent any

    stages{

        stage("Descargar código de la aplicación"){
            steps{
                git "https://github.com/jesuscle/facturas-rest.git"
            } 
        }        

        stage("Creación de imagen"){
            steps{
                script {
                    if(isUnix()){
                        sh "docker build -t jsalinas/facturas-node-16 ."
                    }else{
                        bat "docker build -t jsalinas/facturas-node-16 ."
                    }
                }
                
            } 
        }

       stage("Ejecución de contenedor"){
           steps {
               script {
                    if(isUnix()){
                        sh "docker run -d --name app-facturas-node -p 8081:8080 jsalinas/facturas-node-16"
                    }else{
                        bat "docker run -d --name app-facturas-node -p 8081:8080 jsalinas/facturas-node-16"
                    }
               }
           }
        }

        stage("Test del servicio"){
            steps {
                echo "Probando el servicio ..."
            }
        }

        stage("Cerrar recursos"){
           steps {
               script{
                    if(isUnix()){
                        sh "docker stop app-facturas-node"
                        sh "docker container rm app-facturas-node" 
                        sh "docker image rm jsalinas/facturas-node-16" 
                    }else{
                        bat "docker stop app-facturas-node"
                        bat "docker container rm app-facturas-node" 
                        bat "docker image rm jsalinas/facturas-node-16" 
                    }
               }
            }            
        }
    }
}