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

	stage ('Copy') {
            steps {
                build job: 'Copy-artifacts', parameters: [string(name: 'BRANCH', value: 'master')]
            }
            post {
                always {
				//sh 'cd /var/lib/jenkins/jobs/Multibranch-Pipeline'
				//sh 'pwd'
				dir('/var/lib/jenkins/jobs/Multibranch-Pipeline') {
					dest="/var/lib/jenkins/ravi"
					 //cp -rf  $src $dest
	               			 find ./ -name '*.xml' -exec cp -prv '{}' $dest ';'
				}
           	 }
       	    }
	} 
    }
}
