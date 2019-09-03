pipeline {
    agent none    
    stages {
	    stage('remove_old_code'){
		    agent any
		    steps{
		    dir ('testing-junit5-mockito') {
		    sh 'ssh veso@192.168.1.164 ls'
		    }
		    }
	    }
	    
       
    }

}
