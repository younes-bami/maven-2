podTemplate(containers: [

    containerTemplate(
        name: 'python', 
        image: 'python:latest', 
        command: 'sleep', 
        args: '30d')
  ]) {

   node (POD_LABEL) {
    stage('Main'){
    container ('maven'){
        stage('Build') {
                sh 'mvn -B -DskipTests clean package'
        }
    }
    container('maven'){
        stage('Test') {
                sh 'mvn test'
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }}
        container('maven'){
        stage('Deliver') {
                sh './jenkins/scripts/deliver.sh'
        }
    }
   }
   }
}
