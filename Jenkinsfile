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
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
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
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
