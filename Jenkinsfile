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
                                        sh 'git clone https://github.com/spring-guides/gs-maven.git'
                                        sh 'mvn package /var/lib/jenkins/workspace/test1/*'
                	        }
                              /*  post {
                                        always {
                                                junit 'target/gs-maven-reports/*.xml'
                                        }
                                }  */                
        	}
    }
}
