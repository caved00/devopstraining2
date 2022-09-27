pipeline {
        agent any
/* testing 45 options {
        ansicolor('xterm')
    } */

    environment {
        DOCKERHUB_CREDENTIALS=credentials('caved00')
    }
   
    stages {
        	stage('Build Stage') {
            		steps {
                		script {
                    			echo "albBuild.sonarMavenExec()"
                		}
            		} 
        	}
    }
}
