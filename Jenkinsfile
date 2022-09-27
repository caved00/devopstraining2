pipeline {
        agent any
/* testing options {
        ansicolor('xterm')
    } */

    environment {
        DOCKERHUB_CREDENTIALS=credentials('caved00')
        PATH = "/var/lib/jenkins/workspace/test1/java-maven-junit5-example:$PATH"
    }
   
    stages {
                stage('Code checkout - GITHUB') {
            		        steps   {
                                        git credentialsId: 'github', 'https://github.com/caved00/devopstraining2'                                   
                	        }
                }     
                stage('Build - Maven') {
            		        steps   {
                                        cleanWs()
                                        sh 'git clone https://github.com/bluetata/java-maven-junit5-example.git'
                                        sh 'mvn package'
                                      
                	        }
                } 
                stage('Testing - JUnit testing') {
            		        steps   {
                                        sh 'mvn test -f /var/lib/jenkins/workspace/test1/java-maven-junit5-example/pom.xml'
                                      
                	        }
                        
                              /*  post {
                                        always {
                                                junit 'target/gs-maven-reports/*.xml'
                                        }
                                }  */                
        	}
    }
}
