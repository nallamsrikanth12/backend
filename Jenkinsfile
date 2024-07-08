pipeline {
    agent {
        label 'Agent-1'
    }
    options {
        // Timeout counter starts BEFORE agent is allocated
        timeout(time: 1, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    stages {
        stage('install dependences of the npm ') {
            steps {
                sh """
                 echo this is testing
                 npm install
                """
            }
        }
    }
    post { 
            always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success { 
            echo 'I will run pipe is sucess'
        }
        failure { 
            echo 'I will run pipe is failure'
        }
    
    }

}