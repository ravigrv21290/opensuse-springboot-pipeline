pipeline {
 agent any 

    stages {
		
		stage ('Checkout') {
		
			steps {
			
				git 'https://github.com/ravigrv21290/opensuse-springboot-pipeline.git'
				
			}          

        }
		
        stage ('Compile Stage') {

           

            steps {

                withMaven(maven : 'apache-maven-3.6.0') {

                    sh 'mvn install'               

                }

            }

        }



        stage ('Testing Stage') {



            steps {

                withMaven(maven : 'apache-maven-3.6.0') {

                   sh 'mvn test'

                }

            }

        }





        stage ('Package Stage') {

            steps {

                withMaven(maven : 'apache-maven-3.6.0') {

                    sh 'mvn package'

                }

            }

        }

    }

}
