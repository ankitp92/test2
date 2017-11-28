pipeline {
    agent any


    stages {
        stage('build') {

          steps{
              script{
                  env.branch_pushed="master"
                  sh "printenv"
            }
          }
    }

}
