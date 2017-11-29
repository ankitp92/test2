pipeline {
    agent any


    stages {
        stage('build') {

          when {
            expression {
              return params.SKIP_PnL=="1"
            }
          }

          steps{
              script {
                env.SKIP_PnL="1"
                sh 'printenv'
              }


            }
          }

        stage('JOB_TRIGGER Check') {
          when {
            expression {
              return params.JOB_TRIGGER=="0"
            }
          }

            steps {
              script {
                sh 'printenv'
                result = sh (script: "git log -1 | grep '\\[pnl skip\\]'", returnStatus: true)
                echo "${result}"
                if ( result!=0 ){
                  env.SKIP_PnL="0"
                }else {
                  env.SKIP_PnL="1"
                }
              }
            }

          }

          stage('Check NULL') {
            steps {
              script{
                if(env.SKIP_PnL){
                  echo "${SKIP_PnL}"
                }else {
                  env.SKIP_PnL="0"
                }
              }
            }
          }
      }

        post {
          success {

                node('master') {
                  build job: 'test3', parameters: [[$class: 'StringParameterValue', name: 'SKIP_PnL', value: env.SKIP_PnL]]
                }

              }

          }


}
