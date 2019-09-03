
pipeline {
    agent none
        
    stages {
        
        stage('test') { 
			agent {
                docker { image 'maven:3-alpine' }
            }
            steps {
            
				dir ('testing-junit5-mockito') {
                    sh 'mvn package'
                }
            
            }
            }
            
            
            stage('test1') { 
			
            steps {
            
				dir ('testing-junit5-mockito') {
                    sh 'ssh'
                }
            
            }
            }
            
            }
            }
/** wrong **/
