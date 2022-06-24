podTemplate(containers: [

        containerTemplate(
        name: 'jnlp', 
        image: 'jenkins/inbound-agent:latest', 
        resourceRequestCpu: '500m',
        resourceLimitCpu: '1000m',
        resourceRequestMemory: '500Mi',
        resourceLimitMemory: '1000Mi'
        ),
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
      mountPath: '/root/.m2', 
      claimName: 'maven-m2'      ),
  persistentVolumeClaim(
      mountPath: '/home/jenkins/agent/workspace', 
      claimName: 'maven-workspace'      )
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


