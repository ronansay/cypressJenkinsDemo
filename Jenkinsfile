import groovy.json.JsonOutput

def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]

def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

pipeline {
  agent any

  environment {
        BUILD_USER = ''
    }

  
  tools {nodejs "nodejs21"}

  options {ansiColor('xterm')}

  stages {
     stage('Dependencies') {
        steps {
            bat 'npm i'
        }
     }
     stage('e2e Tests 1') {
        steps {
            bat 'npm run cypress:chrome'
        }
     }
     stage('e2e Tests 2') {
        steps {
            bat 'npm run test'
        }
     }
  }
  post{
    always{

      script {
                BUILD_USER = getBuildUser()
            }

            slackSend channel: '#random',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${BUILD_USER}\n More info at: ${env.BUILD_URL}HTML_20Report/"

      
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
    }
  }
  
   
}
