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
                                        sh 'mvn package'
                	        }
                              /*  post {
                                        always {
                                                junit 'target/gs-maven-reports/*.xml'
                                        }
                                }  */                
        	}
    }
}
