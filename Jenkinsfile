pipeline {
    agent any
    stages {
        stage('Compile') {
            steps {
                echo 'Compiling Code'
		sh 'mvn install -DskipTests -f pom.xml'
            }
        }
        stage('UnitTest') {
            steps {
                echo 'Unit Test'
		sh 'mvn test -f pom.xml'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scan Vulnerability'
            }
        }
        stage('BuildApp') {
            steps {
                echo 'BuildApp'
		sh 'mvn package -f pom.xml'
            }
	    post{
	    success{
            archiveArtifacts artifacts: '**/**/*.war', followSymlinks: false
	    }
        }
	}
       stage('PushImage') {
            steps {
                echo 'Push image to registry'
            }
        } 
    }
}

