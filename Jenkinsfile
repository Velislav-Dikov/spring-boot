
pipeline {
    agent none    
    stages {
        stage('build_and_test') { 
		agent {
                	docker { image 'maven:3-alpine' }
		}
	steps {
		dir ('testing-junit5-mockito') {
                    sh 'mvn test package'
                }
            }
        }
            stage('Deploy_and_restart') { 
		agent any
            	steps {
            		dir ('testing-junit5-mockito') {
                	    sh 'scp -r target veso@192.168.1.130:/home/veso/Downloads'
			    sh 'ssh veso@192.168.1.130 sudo systemctl restart java-app'
                }
            }
        }
    }
	   post {
	agent any
      always {
        junit '**/reports/junit/*.xml'
      }
   } 
}


/** works **/
