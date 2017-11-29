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
              script {
                env.SOURCE_BRANCH="master"
                sh 'printenv'
              }


            }
          }

        stage('branch check') {
            when {
              branch "test"
            }

            steps {
              script{
                env.SOURCE_BRANCH="test"
              }
            }

          }

        post {
          success {

              node('master') {
                build job: 'test3', parameters: [[$class: 'StringParameterValue', name: 'SOURCE_BRANCH', value: env.SOURCE_BRANCH]]
              }

          }

    }

}
