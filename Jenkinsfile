pipeline {
    agent any

    parameters {
      string( defaultValue:'0', description:'', name:'JOB_TRIGGER')
      string( defaultValue:'0', description:'', name:'SKIP_PnL')
    }


    stages {


        stage('JOB_TRIGGER Check') {

            steps {
              script {
                  echo "${SKIP_PnL}"
                  if("${JOB_TRIGGER}"==0){
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


      }

        post {
          success {

                node('master') {
                  build job: '../test3/master', parameters: [[$class: 'StringParameterValue', name: 'SKIP_PnL', value: "${SKIP_PnL}"]]
                }

              }

          }


}
