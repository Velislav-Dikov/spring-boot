pipeline {
    agent none    
    stages {
	    stage('remove_old_code'){
		    sleep(time:10,unit:"SECONDS")
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
			    sh 'ssh veso@192.168.1.130 sudo systemctl stop java-app'
			    sh 'ssh veso@192.168.1.130 rm -rf /home/veso/Downloads/target'
			    sh 'scp -r target veso@192.168.1.130:/home/veso/Downloads'
			    sh 'ssh veso@192.168.1.130 sudo systemctl start java-app'
                }
            }
        }
        
        stage('app_test') { 
			agent any
			steps{
		                sleep(time:10,unit:"SECONDS")
		                sh 'curl -v 192.168.1.130:8080'
		                sh 'ssh veso@192.168.1.130 sudo systemctl status java-app'
				
		        
		    }
	}
       
    }

}
