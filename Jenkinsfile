pipeline {
    agent { label "built-in" }
        triggers {
        pollSCM('H/2 * * * *')    
                }
            stages {
        stage('build') {
                steps {
                sh 'docker --version'
                        }
                }
                    }
        }
