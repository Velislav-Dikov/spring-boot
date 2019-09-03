pipeline {
    agent none    
    stages {
	    stage('remove_old_code'){
		    agent any
		    steps{
		    dir ('testing-junit5-mockito') {
		    sh 'rm -rf target'
		    }
		    }
	    }
	    stage('build_and_test') { 
			agent any
			steps{
		    dir ('testing-junit5-mockito') {
		    sh 'mvn test'
		    sh 'mvn package'
		    sh 'mvn surefire-report:report'  
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

}
