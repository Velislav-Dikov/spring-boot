pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('move') { 
            steps {
                dir ('testing-junit5-mockito') {
                    sh 'mvn test'
                }
                
                 dir ('testing-junit5-mockito') {
                    sh 'mvn package'
                }
            }
        }        
    }
}
