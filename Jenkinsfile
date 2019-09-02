pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('test') { 
            steps {
                dir ('testing-junit5-mockito') {
                    sh 'ssh veso@192.168.1.130 ls /home/veso/.ssh'
                }
            }
        }        
    }
}
