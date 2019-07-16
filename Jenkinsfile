pipeline {
 agent any
	
 environment {
    EMAIL_RECIPIENTS = 'rvgrv212@gmail.com'
	 def server
	def buildInfo
	def rtMaven

 }

    stages {	
	stage ('Checkout') {	
		steps {
			echo 'Pulling...' + env.BRANCH_NAME
			git 'https://github.com/ravigrv21290/opensuse-springboot-pipeline.git'	
		}          
        }
	
        stage ('Compile Stage') {
            steps {
		   sh 'mvn clean install'        
            }
        }
	    
        stage ('Testing Stage') {
            steps {
            	sh 'mvn test'
            }
        }

        stage ('Package Stage') {
            steps {
		sh 'mvn package'
            }
        }
	    
	stage ('Sonar Analysis Stage') {
            steps {
		sh 'mvn sonar:sonar -Dsonar.host.url=http://ds-ina750qs6c:9000/sonar'
            }
        }
	    
	stage ('Artifactory Configuration Stage') {
            steps {
		// Obtain an Artifactory server instance, defined in Jenkins --> Manage:
        	server = Artifactory.server SERVER_ID
	        rtMaven = Artifactory.newMavenBuild()
        	rtMaven.tool = maven // Tool name from Jenkins configuration
        	rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
        	rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
        	rtMaven.deployer.deployArtifacts = false // Disable artifacts deployment during Maven run	
       		buildInfo = Artifactory.newBuildInfo()
            }
        }
	    
	stage ('Deploy Stage') {
            steps {
		sh 'mvn deploy'
            }
        }
    }
	post {
        	always {
            		echo 'Copying artifacts'
			//archiveArtifacts 'target/surefire-reports/*.xml'
		
	    	// It takes all files from source like .java,.class,.jar,xml etc
		// archive '**'  
		
		// takes all .xml files
		// archive '**/*.xml'
		
		archive 'target*//*.jar'
		// copy only target files
		
		//copyArtifacts filter: 'target*//*.jar', fingerprintArtifacts: true, projectName: 'Multibranch-Pipeline/master', target: '/var/lib/jenkins/ravi'
		//copyArtifacts filter: 'target/surefire-reports/*.xml', fingerprintArtifacts: true, flatten: true, projectName: 'Multibranch-Pipeline/master', target: '/var/lib/jenkins/ravi'	
		//copyArtifacts filter: '', fingerprintArtifacts: true, flatten: true, projectName: 'Multibranch-Pipeline/master', target: '/var/lib/jenkins/ravi'	

		}
        	success {
            		echo 'I succeeeded!'
        	}
        	unstable {
            		echo 'I am unstable :/'
        	}
        	failure {
            		echo 'I failed :('
        	}
	}	
}
