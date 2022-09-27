pipeline {
        agent any
/* testing 45 options {
        ansicolor('xterm')
    } */

    environment {
        DOCKERHUB_CREDENTIALS=credentials('caved00')
    }
   
    stages {
        	stage('Build, Test21 & SonarQube Analysis') {
            		steps {
                		script {
                    			echo "${env.imageURI}"
                    			echo "albBuild.sonarMavenExec()"
                		}
            		} 
        	}
    }
}
