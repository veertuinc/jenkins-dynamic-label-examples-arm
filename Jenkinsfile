def AGENT_LABEL = createDynamicAnkaNode(
  masterVmId: '9bf0318f-5c58-4142-b544-cf743a087a41',
  tag: 'v1',
  launchMethod: 'ssh',
  credentialsId: 'anka',
  nameTemplate: 'nested-cache-builder-failing-example'
)
def NESTED_LABEL = ''

pipeline {
  agent {
    label "${AGENT_LABEL}"
  }
  stages {
    stage("command-in-AGENT_LABEL-vm") {
      steps {
        sh "uname -a" // Run within the first AGENT_LABEL VM instance
      }
    }
    stage("nested-vm-stages") {
      stages {
        stage("launch-nested-vm") { // Creates a second VM instance which will, after job completion, push to the Registry.
          steps {
            script {
              NESTED_LABEL = createDynamicAnkaNode(
                launchMethod: 'jnlp', 
                masterVmId: '9bf0318f-5c58-4142-b544-cf743a087a41',
                tag: 'v1',
                nameTemplate: 'nested-failing-example-nested',
                saveImage: true, 
                suspend: true,
                deleteLatest: true // Dangerous: only use if the Template isn't holding other project tags.
              )
            }
          }
        }
        stage("run-on-NESTED_LABEL-vm") {
          agent { label "${NESTED_LABEL}" }
          steps {
            // If buildResults == 'FAILURE', Anka will not push the NESTED_LABEL VM. Example:
            catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
              sh 'uname -x'
            }
          }
        }
        stage("check-generated-tag-from-nested-vm") {
          steps {
            script {
              def getPushResult = ankaGetSaveImageResult( shouldFail: true, timeoutMinutes: 120 )
              echo "ankaGetSaveImageResult Returned: $getPushResult"
            }
          }
        }
      }
    }
  }
}
