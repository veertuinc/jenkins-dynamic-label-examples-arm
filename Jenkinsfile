pipeline {
  agent {
   label createDynamicAnkaNode(
      masterVmId: '9bf0318f-5c58-4142-b544-cf743a087a41',
      tag: 'v1',
      nameTemplate: 'simple-example'
    )
  }
   stages {
     stage("hello") {
       steps {
         sh "echo hello; sleep 120"
       }
     }
  }
}
