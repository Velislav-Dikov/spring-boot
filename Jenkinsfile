
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
			agent any
            steps {
            
				dir ('testing-junit5-mockito') {
                    sh 'scp -r veso@192.168.1.130:/home/veso/Downloads'
                }
            
            }
            }
            
            }
}
/**wrong**/
