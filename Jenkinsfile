def config = {}
def env = {}
pipeline {
  agent any
  triggers{
    pollSCM('H/2 * * * *')
  }
  stages {
    stage("Configuration setup..."){
            steps{
                echo "Configuration setup..."
                script{
                    config = readJSON file:"env/${env.BRANCH_NAME}/config.json"
                    env = config.get("envConfig")
                }
            }
    }
stage('Build Application') {
      steps {
        sh 'mvn clean install'
      }  
    }
    stage('Deploy CloudHub') {
      environment {
        ANYPOINT_CREDENTIALS = credentials('f18a5dbc-e6e4-45d4-90e4-bc0cfd9e3a7f')
      }
      steps {
        sh "mvn deploy -DmuleDeploy -Dcloud.env=${env.envName} -DcloudhubAppName=${env.cloudhubAppName} -Dmule.version=${env.muleVersion} -Dcloud.user=${ANYPOINT_CREDENTIALS_USR} -Dcloud.password=${ANYPOINT_CREDENTIALS_PSW}"
      }
    }
  }
}
