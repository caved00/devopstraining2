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
                                        sh 'git clone https://github.com/LableOrg/java-maven-junit-helloworld.git'
                                        sh 'mvn package -f /var/lib/jenkins/workspace/test1/gs-maven/initial/pom.xml'
                                      
                	        }
                 
                stage('Testing - JUnit testing') {
            		        steps   {
                                        sh 'mvn test -f /var/lib/jenkins/workspace/test1/gs-maven/'
                                      
                	        }
                        
                              /*  post {
                                        always {
                                                junit 'target/gs-maven-reports/*.xml'
                                        }
                                }  */                
        	}
    }
}
