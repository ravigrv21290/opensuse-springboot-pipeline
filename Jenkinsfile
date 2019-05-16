pipeline {
 agent any 

 environment {
    EMAIL_RECIPIENTS = 'rvgrv212@gmail.com'
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
    }
	post {
        always {
            echo 'Copying artifacts'
		archive 'target*//*.jar'
		
		

		
	    	// It takes all files from source like .java,.class,.jar,xml etc
		// archive '**'  
		
		// takes all .xml files
		// archive '**/*.xml'
		
		//archive 'target*//*.jar'
		// copy only target files
		
		//copyArtifacts filter: 'jobs/Multibranch-Pipeline/*.xml', fingerprintArtifacts: true, projectName: 'Multibranch-Pipeline/master', target: '/opt/jenkins-config-artifacts/'
		sh 'cd /var/lib/jenkins/jobs/Multibranch-Pipeline'
		sh 'pwd'
		sh 'find . -name '*.txt' | cpio -pdm /opt/jenkins-config-artifacts'
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
