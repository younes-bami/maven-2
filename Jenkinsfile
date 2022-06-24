podTemplate(containers: [

    containerTemplate(
        name: 'maven', 
        image: 'maven:latest', 
        command: 'sleep', 
        args: '30d',
        resourceRequestCpu: '500m',
        resourceLimitCpu: '1000m',
        resourceRequestMemory: '500Mi',
        resourceLimitMemory: '1000Mi')
  ],
  volumes: [
  persistentVolumeClaim(
      mountPath: '/home/vagrant/.m2/repository', 
      claimName: 'maven-m2'      )
  ]
  
  ) {

    node(POD_LABEL) {
        stage('Get a Python Project') {
            git url: 'https://github.com/younes-bami/maven-2.git', branch: 'master'

            container('maven') {
                stage('Build') {
                    sh '''
                        mvn -B -DskipTests clean package                    
                        '''
                }
            }
            container ('maven'){
                stage('Test'){
                    sh '''
                        mvn test

                       '''


                }
            }
            container ('maven'){
                stage('Deliver'){
                    sh '''
                        ./jenkins/scripts/deliver.sh
                       '''


                }
            }
        }

    }
}


