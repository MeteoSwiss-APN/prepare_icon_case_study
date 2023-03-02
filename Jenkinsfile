pipeline {

    options {

        disableConcurrentBuilds()
        buildDiscarder(logRotator(artifactDaysToKeepStr: '7', artifactNumToKeepStr: '7',
                                  daysToKeepStr: '7', numToKeepStr: '7'))
        timeout(time: 48, unit: 'HOURS')
    }
    environment {
      JENKINS_DIR = "$workspace"
        
    }
    stages {
        stage('Run script') {
            steps {
                sh '''
                        prepare_case_study.sh 23030100 2
                    '''
                
            }
            
        }
        stage('Test') {
          steps {
                    sh '''
                    [ "$(find ${JENKINS_DIR}/output_icon/23030100 -name efsf00000000_lbc.nc)" ] && find ${JENKINS_DIR}/output_icon/23030100 -name efsf00000000_lbc.nc || (echo "No boundary file found in output folder" && exit 1) 
                    [ "$(find ${JENKINS_DIR}/output_icon/23030100 -name laf2023030100.*)" ] && find ${JENKINS_DIR}/output_icon/23030100 -name laf2023030100.* || (echo "No analysis file found in output folder" && exit 1) 


                       '''
                
            }
        }
    }
    post {
        always {
            echo "Build stage complete"
        }
        failure {
            echo "Build failed"
            emailext(subject: "${currentBuild.fullDisplayName}: ${currentBuild.currentResult}",
                     body: """Job '${env.JOB_NAME} #${env.BUILD_NUMBER}': ${env.BUILD_URL}""",
                     recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']])
        }
        success {
            echo "Build succeeded"
        }
        cleanup {
            sh """
            rm -rf ${JENKINS_DIR}/output_icon/23030100
    
            """
        }
    }
}
