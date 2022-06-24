podTemplate(containers: [

    containerTemplate(
        name: 'maven', 
        image: 'maven:latest', 
        command: 'sleep', 
        args: '30d')
  ]) {

    node(POD_LABEL) {
        stage('Get a Python Project') {
            git url: 'https://github.com/younes-bami/maven-2.git', branch: 'master'

            container('maven') {
                stage('Build') {
                    sh '''
                        mvn -B -DskipTests clean package                    
                        '''
                }
                stage('Test'){
                    sh '''
                        mvn test

                       '''
                }
            }
        }

    }
}


