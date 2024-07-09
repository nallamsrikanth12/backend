pipeline {
    agent {
        label 'Agent-1'
    }
    options {
        // Timeout counter starts BEFORE agent is allocated
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment {
        def appversion = '' // variable declaration
        nexusUrl = 'nexus.srikantheswar.online:8081'
    }

    stages {
        stage('read the json files') {
            steps {
                script {
                    def packagejson = readJSON file: 'package.json'
                    appversion = packagejson.version
                    echo "application version : ${appversion}"
                }
            }
        }
        stage('install dependencies of the npm') {
            steps {
                sh """
                    echo this is testing
                    npm install
                    ls -ltr
                    echo "application version : ${appversion}"
                """
            }
        }
        stage('Build') {
            steps {
                sh """
                    zip -q -r backend.${appversion}.zip * -x jenkinsfile -x backend.${appversion}.zip
                    ls -ltr
                """
            }
        }
        stage('Nexus artifacts uploader') {
            steps {
                script {
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${nexusUrl}",
                        groupId: 'com.expense',
                        version: "${appversion}",
                        repository: 'backend',
                        credentialsId: 'nexus-auth',
                        artifacts: [
                            [
                                artifactId: "backend",
                                classifier: '',
                                file: "backend.${appversion}.zip",
                                type: 'zip'
                            ]
                        ]
                    )
                }
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success { 
            echo 'I will run pipeline is success'
        }
        failure { 
            echo 'I will run pipeline is failure'
        }
    }
}
