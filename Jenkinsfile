pipeline {
        agent any
/* testing options {
        ansicolor('xterm')
    } */

    environment {
        DOCKERHUB_CREDENTIALS=credentials('caved00')
    }
   
    stages {
                stage('Build - Maven') {
            		        steps   {
                                        cleanWs()
                                        sh 'git clone https://github.com/bluetata/java-maven-junit5-example.git'
                                        sh 'mvn package -f /home/ir00at/mavenbuild/java-maven-junit5-example/pom.xml'
                                      
                	        }
                 
                stage('Testing - JUnit testing') {
            		        steps   {
                                        sh 'mvn test -f /var/lib/jenkins/workspace/test1/gs-maven/pom.xml'
                                      
                	        }
                        
                              /*  post {
                                        always {
                                                junit 'target/gs-maven-reports/*.xml'
                                        }
                                }  */                
        	}
    }
}
