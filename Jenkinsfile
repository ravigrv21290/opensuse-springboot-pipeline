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

	stage ('archieve') {

            steps {
                archiveArtifacts artifacts: '/target/*.jar', fingerprint: true

            }
        }

    }
}
