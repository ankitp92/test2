pipeline {
    agent any


    stages {
        stage('build') {

          when {
            SOURCE_BRANCH "master"
          }

          steps{

              sh 'printenv'

            }
          }
    }

}
