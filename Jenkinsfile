pipeline {
    agent any
    stages{

        stage("Descargar código de la aplicación"){
            steps{
                git "url"
            } 
        }        

        stage("Creación de imagen"){
            steps{
                sh "docker build -t jsalinas/app1 ."
            } 
        }

       stage("Ejecución de contenedor"){
           steps {
               sh "docker run -d --name app1 -p 8081:8080 jsalinas/app1"
           }
           
        }

        stage("Test del servicio"){
            steps {
                echo "Probando el servicio ..."
            }
        }

        stage("Cerrar recursos"){
           steps {
                sh "docker stop app1"
                sh "docker container rm app1" 
                sh "docker image rm jsalinas/app1" 
            }            
        }
    }
}