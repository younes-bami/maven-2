pipeline {
agent {
    node { label 'java-build' 
            } 
    }
   stages {
        stage('Hello-world'){

            agent { docker { image 'hello-world' } }

            steps{
                    sh '''
                    echo 'hello my world'
                    '''
            }
        }
        stage('Build') {
            agent {
    node { label 'java-build' 
            } 
    }
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            agent {
    node { label 'java-build' 
            } 
    }
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            agent {
    node { label 'java-build' 
            } 
    }
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
