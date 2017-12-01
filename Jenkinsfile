pipeline {
    agent any


    stages {


        stage('JOB_TRIGGER Check') {
          when {
            expression {
              return "${JOB_TRIGGER}"=="0"
            }
          }

            steps {
              script {
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

          stage('Check NULL') {
            steps {
              script{
                if($SKIP_PnL){
                  echo "${SKIP_PnL}"
                }else {
                  SKIP_PnL="0"
                }
              }
            }
          }
      }

        post {
          success {

                node('master') {
                  build job: 'test3', parameters: [[$class: 'StringParameterValue', name: 'SKIP_PnL', value: $SKIP_PnL]]
                }

              }

          }


}
