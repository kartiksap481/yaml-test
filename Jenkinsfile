pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    DB_CREDS = credentials('db-cred-user')
    MULE_VERSION = '4.3.0'
    BG = "Apisero"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          bat "mvn test"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'Sbx-mule-yaml'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%" -Denv.host="db4free.net" -Denv.user="%DB_CREDS_USR%" -Denv.password="%DB_CREDS_PSW%" -Denv.database="yamltest" -Denv.port="3306" '
      }
    }
    
  }


}
