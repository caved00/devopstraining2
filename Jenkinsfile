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
                                        cleanWs()
                                        sh 'git clone https://github.com/spring-guides/gs-maven.git'
                                        dir("${env.WORKSPACE}@tmp")
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
