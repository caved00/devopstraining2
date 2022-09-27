pipeline {
        agent any
/* testing options {
        ansicolor('xterm')
    } */

    environment {
        DOCKERHUB_CREDENTIALS=credentials('caved00')
    }
   
    stages {
        	stage('Clone Repo') {
            		        steps   {
                                        sh 'rm -rf "/var/lib/jenkins/workspace/test1/*"'
                                        sh 'git clone https://github.com/spring-guides/gs-maven.git'
                                        sh 'mvn package -f /var/lib/jenkins/workspace/test1/gs-maven/initial/pom.xml'
                                      
                	        }
                              /*  post {
                                        always {
                                                junit 'target/gs-maven-reports/*.xml'
                                        }
                                }  */                
        	}
    }
}
