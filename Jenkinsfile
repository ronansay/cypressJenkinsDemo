pipeline {
  agent any
  
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
  
   
}