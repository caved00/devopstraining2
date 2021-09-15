pipeline {
        agent any
/*    options {
        ansicolor('xterm')
    } */

    environment {
        DOCKERHUB_CREDENTIALS=credentials('caved00')
        /* registry = "caved00/a-team_repo01" 
        registryCredential = 'caved00' 
        dockerImage = '' 
        registry              = "escoacrprod01.azurecr.io"
        registryCredential      = 'acr_creds_esco_prod'
        dockerfile              = 'Dockerfile'
        registryRepo            = "/rcdo/rcdo-ant"
        CommitId                = 'False'
        imageURI                = "${registry}${registryRepo}:${env.BUILD_NUMBER}"
        VeraAppid               = "rcdo-prod-${env.BUILD_NUMBER}"
        VeraAppName             = "RCDO"
        AbortOnFaile            = "false"
        CompliancePolicy        = 'warn'
        VulnerabilityPolicy     = 'warn'
        RemoveImageOnPublish    = false
        loglevel                = 'debug' */ 
    }
   
    stages {
        	stage('Build, Test & SonarQube Analysis') {
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
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

/*
	        stage('Docker push image to Dockerhub') {
       		     steps {
               		     sh 'docker push caved00/a-team_repo01:latest'
            		}
        	}
*/

        	stage('Twistlock Analysis') {
            		steps {
                		script {
                    			echo "albBuild.twistscanDockerImage(imageURI, loglevel)"
                		}
            		}
        	}
    
		stage('Push image to Dockerhub') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}
        
        
        /*
        post {
            failure {
                script {
                    echo "albNotify.emailNotify()"
                }
            }
        }
        */
    }
}
