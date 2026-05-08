pipeline {
    agent any
    stages {
        stage('Compile') {
            steps {
                echo 'Compiling Code'
            }
        }
        stage('UnitTest') {
            steps {
                echo 'Unit Test'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scan Vulnerability'
            }
        }
        stage('QualityGate') {
            steps {
                echo 'QGate'
            }
        }
        stage('CreateImage') {
            steps {
                echo 'Creating docker image'
            }
        }
       stage('PushImage') {
            steps {
                echo 'Push image to registry'
            }
        } 
    }
}

