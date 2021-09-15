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
        /* when { allOf { environment name: 'application_type', value: 'java' } } */
            steps {
                script {
                    echo "${env.imageURI}"
                    echo "albBuild.sonarMavenExec()"
                }
            }
        }
        
        stage('Build, Test, Coverage and sonar') {
        /* when { allOf { environment name: 'application_type', value: 'nodejs' } } */
            steps {
                script {
                    echo "albBuild.npmHeadless()"
                }
            }
        }
        
        stage('SonarQube Quality Gate') {
        /* when { allOf { environment name: 'application_type', value: 'java' } } */
            steps {
                script {
                    echo "albBuild.sonarQualityGate(AbortOnFail)"
                }
            }
        }
        
        stage('Veracode Scan') {
        /* when { allOf { environment name: 'application_type', value: 'java' } } */
            steps {
                script {
                    echo "albBuild.veraCodeScanwar(VeraAppid, AbortOnFail, VeraAppName)"
                }
            }
        }
        
        stage('Veracode nodejs Scan') {
        /* when { allOf { environment name: 'application_type', value: 'nodejs' } } */
            steps {
                script {
                    echo "sh tar -czvf node_modules.tar.gz node_modules"
                    echo "albBuild.veraCodeScannj(VeraAppid, AbortOnFail, VeraAppName)"
                }
            }
        }
        
        /* stage('Docker build image') {
            steps {
                script {
                    echo "dockerImage = albBuild.buildDockerTaggedImage(registry, registryRepo, dockerfile)"
                }
            }
        } */


        /* stage('Docker build image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        } */

		stage('Docker build image and login to docker hub') {

			steps {
				sh 'docker build -t getting-started .'
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

/*		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}
*/

/*        stage('Docker push image to Dockerhub') {
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
    
    /* Push to image registry 
        stage('Docker push image to ACR') {
            steps {
                script {
                    echo "albBuild.publishDockerImage(registry, registryCredential, dockerImage, imageURI, removeAfterPublish = RemoveImageOnPublish)"
                }
            }
        } */


        
        
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
