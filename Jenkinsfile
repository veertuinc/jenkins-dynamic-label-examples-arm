def label = createDynamicAnkaNode(
  masterVmId: '9bf0318f-5c58-4142-b544-cf743a087a41',
  tag: 'v1',
  nameTemplate: 'scripted-example'
)

node(label){
    stage('Sleep') { 
        sh 'sleep 120'
    }
    stage('Do something') { 
        sh 'echo hello'
    } 
}
