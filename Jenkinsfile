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
	stage('Build docker image') {
            steps {
                sh 'docker image build -t registry.local/java-app:$BUILD_NUMBER .'
            }
        }

       stage('PushImage') {
            steps {
                echo 'Push image to registry'
            }
        } 

	stage('Deploy to Stagging Env') {
            steps {
                echo 'Running app on stagging env'
		sh '''
		docker stop tomcatInstanceStaging || true
		docker rm tomcatInstanceStaging || true
	docker run -itd --name tomcatInstanceStaging -p 8083:8080 registry.local/java-app:$BUILD_NUMBER
	sh '''
            }
        }
	
	stage('Deploy Production Environment'){
	steps{
	timeout(time:1, unit:'DAYS'){
	input message: 'Approve PRODUCTION Deployment?'
	}
	echo "Running app on Prod env"
	sh '''
	docker stop tomcatInstanceProd || true
        docker rm tomcatInstanceProd || true
        docker run -itd --name tomcatInstanceProd -p 8084:8080 registry.local/java-app:$BUILD_NUMBER
        sh '''
       }
      
      }

    }
}

