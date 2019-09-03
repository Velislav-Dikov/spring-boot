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
		agent {
			dir ('testing-junit5-mockito') {
                    sh 'mvn test'
		    sh 'mvn package'
                }
			
		}
		}
       
    }

}
