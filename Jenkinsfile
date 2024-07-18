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
     stage('e2e Tests') {
        steps {
            bat 'npm run cypress:chrome'
        }
     }
  }
  
   
}