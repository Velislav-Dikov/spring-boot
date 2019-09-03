pipeline {
    agent any    
    stages {
	    stage('remove_old_code'){
		    steps{
		    dir ('testing-junit5-mockito') {
		    sh 'rm -rf target'
		    }
		    }
	    }
	    stage('build_and_test') { 
		    steps{
		    dir ('testing-junit5-mockito') {
		    sh 'mvn test'
		    sh 'mvn package'
		    sh 'mvn surefire-report:report' 
		     
		    }
		    
		  }
		}
		
		stage('Deploy_and_restart') { 
		   	steps {
            		dir ('testing-junit5-mockito') {
			    sh 'ssh veso@192.168.1.130 sudo systemctl stop java-app'
			    sh 'ssh veso@192.168.1.130 rm -rf /home/veso/Downloads/target'
			    sh 'scp -r target veso@192.168.1.130:/home/veso/Downloads'
			    sh 'ssh veso@192.168.1.130 sudo systemctl start java-app'
                }
            }
        }
        
        stage('app_test_and_moving_reports') {
			steps{
			dir ('testing-junit5-mockito') {
		                sleep(time:20,unit:"SECONDS")
				touch 'java-app-report.html'
				sh 'echo "-----------------------------Service status---------------------------------" >> java-app-report.html'
				sh 'ssh veso@192.168.1.130 sudo systemctl status java-app >> java-app-report.html'
				sh 'echo "------------------------ ---Curl test result--------------------------------" >> java-app-report.html'
				sh 'curl -v 192.168.1.130:8080 >> java-app-report.html'
				sh 'mv java-app-report.html target/site'
			}
		        
		        }
      		}
	  }
post {         
        always { 
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'testing-junit5-mockito/target/site', reportFiles: 'surefire-report.html', reportName: 'HTML Report', reportTitles: ''])
        }
    }
}
