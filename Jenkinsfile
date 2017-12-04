pipeline {
    agent any

    properties([
      [$class: 'ParametersDefinitionProperty',
        parameterDefinitions: [
          [$class: 'StringParameterDefinition',
            name: 'JOB_TRIGGER',
            defaultValue: '0',
            description: 'A test parameter']]
      ]
    ])


    stages {


        stage('JOB_TRIGGER Check') {

            steps {
              script {
                  try{
                    echo "${JOB_TRIGGER}"
                  }
                  catch (e){
                    sh 'printenv'
                    result = sh (script: "git log -1 | grep '\\[pnl skip\\]'", returnStatus: true)
                    echo "${result}"
                    if ( result!=0 ){
                      SKIP_PnL="0"
                    }else {
                      SKIP_PnL="1"
                    }
                  }

                }
            }

          }


      }

        post {
          success {

                node('master') {
                  build job: '../test3/master', parameters: [[$class: 'StringParameterValue', name: 'SKIP_PnL', value: "${SKIP_PnL}"]]
                }

              }

          }


}
