pipeline {
  agent none
  stages {
    stage('Begin parallel stage1 execution') {
      parallel {
        stage("parallel builder1 command1") {
          agent {
            label createDynamicAnkaNode(
              masterVmId: '9bf0318f-5c58-4142-b544-cf743a087a41',
              tag: 'v1',
              nameTemplate: 'simple-parallel-example-builder1'
            )
          }
          steps {
            echo "builder1 - command1"
            sh "hostname; sleep 120;"
          }
        }
        stage("parallel jenkins host command1") {
          steps {
            echo "jenkins host command 1"
          }
        }
        stage("concurrent builder2 command1") {
          agent { 
            label createDynamicAnkaNode(
              masterVmId: '9bf0318f-5c58-4142-b544-cf743a087a41',
              tag: 'v1',
              launchMethod: 'ssh',
              credentialsId: 'anka',
              nameTemplate: 'simple-parallel-example-builder2'
            )
          }
          steps {
            echo "builder2 - command1"
            sh "hostname; sleep 60;"
          }
        }
      }
    }
  }
}
