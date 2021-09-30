pipeline {
        agent any
/* testing options {
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
        
        	stage('Build, Test, Coverage and sonar') {
            		steps {
                		script {
                    			echo "albBuild.npmHeadless()"
                		}
            		}
        	}
        
        	stage('SonarQube Quality Gate') {
            		steps {
                		script {
                    			echo "albBuild.sonarQualityGate(AbortOnFail)"
                		}
            		}
        	}
        
        	stage('Veracode nodejs Scan') {
            		steps {
                		script {
                    			echo "sh tar -czvf node_modules.tar.gz node_modules"
                    			echo "albBuild.veraCodeScannj(VeraAppid, AbortOnFail, VeraAppName)"
                		}
            		}
        	}
        
		stage('Docker build image and login to docker hub') {
			steps {
				sh 'docker build -t getting-started .'
			}
		}

        	stage('Twistlock Analysis') {
            		steps {
                		script {
                    			echo "albBuild.twistscanDockerImage(imageURI, loglevel)"
                		}
            		}
        	}
    
		stage('Push image to Dockerhub') {
			steps {
               		     	echo 'sh docker push caved00/a-team_repo01:latest'
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}
    }
}
