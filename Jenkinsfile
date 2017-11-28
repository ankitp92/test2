pipeline {
    agent any


    stages {
        stage('build') {

          when {
            expression {
              return params.SOURCE_BRANCH=="master"
            }
          }

          steps{

              sh 'printenv'

            }
          }
    }

}
