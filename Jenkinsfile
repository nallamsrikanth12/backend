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
        stage('read the json files') {
            steps {
                script {
                    def packagejson = readJSON file: 'dir/input.json'
                    def appversion = packagejson.version
                    echo "application version : $appversion"
                }
            }
        }
        stage('install dependences of the npm ') {
            steps {
                sh """
                 echo this is testing
                 npm install
                 ls -ltr
                echo "application version : $appversion"
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