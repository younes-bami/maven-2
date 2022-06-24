podTemplate(containers: [

    containerTemplate(
        name: 'python', 
        image: 'python:latest', 
        command: 'sleep', 
        args: '30d')
  ]) {

   node (POD_LABEL) {

    container (maven){
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }   
                    }
    container (maven){
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
                    }
    container (maven) {
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
                    }            
    }
}
