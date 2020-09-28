 pipeline {
    agent none

    stages {
            stage("Build and start test image") {
             agent {
                label "linux-slave1"
            }
                steps {
                    sh "cd data"
                    sh "docker-compose build"
                    sh "docker-compose up -d"
                }
            }
         stage('Back-end build') {
            agent {
                docker { 
                    image 'maven'
                    label 'master'  
                    args '-u root'
                 }
            }
            steps {
                sh 'mvn clean package'
                sh "docker cp ./var/pet/target/spring-petclinic-2.3.0.BUILD-SNAPSHOT.jar 127.0.0.1:8123/pet.jar"
            }
         }
    }
 }


