podTemplate(containers: [

    containerTemplate(
        name: 'maven', 
        image: 'maven:latest', 
        command: 'sleep', 
        args: '30d')
  ]) {

    node(POD_LABEL) {
        stage('Get a Python Project') {
            container('maven') {
                stage('Build') {
                    sh '''
                        mvn -B -DskipTests clean package                    
                        '''
                }
            }
        }

    }
}


