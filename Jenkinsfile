#!/usr/bin/env groovy

class App {
  String repo
  String repoBranch
  String repoKey
  String service
  String cfgRepo
  String cfgBranch
  String chartType
  String country

  String getConfigRepo() {
    'configs' + service
  }

  String helmStagingValuesFilename() {
    'staging-' + service + '-' + repo + '-' + country + '.yaml'
  }

    //for( String values : str )
    //  echo values

//    if (action.size == 3)
//      str[2]
//    else
//      'error'
}


class AppUtils {

  static String build(String userAction, appMap) {
    //String actionService = AppUtils.getActionService(userAction)
    String actionService = 'eg'
    if (actionService != '*') {
      echo '====== BUILD FOR ALL SERVICES ======'
      for( App app : appMap ) {
        echo '--> ' + app.helmStagingValuesFilename()
      }
      echo '===================================='
    } else {
      echo actionService
    }
  }

  // TARGET: ['staging'|'production']
  static String getActionTarget(String action) {
    String[] str = action.split('-')
    str[0]
  }

  // SERVICE: ['*'|'one'|'flights'|'jforce']
  static String getActionService(String action) {
    String[] str = action.split('-')
    str[1]
  }

  // COUNTRY: ['*'|'ci'|'eg'|'ke'|'ma'|'ng']
  static String getActionCountry(String action) {
    String[] str = action.split('-')
    str[2]
  }
}


//String buildApp(String userAction, def appMap)

// 'staging-*-*'
// 'production-*-*'

def appMap = [:]
appMap['staging-one-ng'] = new App(
  repo:       'daenerys',
  repoBranch: 'dev',
  repoKey:    '20e0cddc-61b3-40c3-a6bc-f630d210b518',
  service:    'one',
  cfgRepo:    'configsone',
  cfgBranch:  'dev',
  chartType:  'raw',
  country:    'ng'
)

appMap['staging-one-eg'] = new App(
  repo:       'daenerys',
  repoBranch: 'dev',
  repoKey:    '20e0cddc-61b3-40c3-a6bc-f630d210b518',
  service:    'one',
  cfgRepo:    'configsone',
  cfgBranch:  'production',
  chartType:  'raw',
  country:    'eg'
)


// ====================== PIPELINE ========================
pipeline {
  agent any
  stages {

    // BUILD
    stage('Build') {
      when {
        expression {
          action.startsWith("staging")
        }                
      }
      steps {
        echo 'Building'
//        echo appMap.get(action)
//        echo appMap.get(action).repo
//        echo "### SERVICE: " + appMap.get(action).getService()

        echo AppUtils.build(action, appMap)

//        sh 'npm --version'
      }
    }
    
    // TEST
    stage('Test') {
      when {
        environment name: 'RUN_TESTS', value: 'true'
      }
      steps {
        echo 'Testing'
      }
    }
    
    // DEPLOY TO STAGING
    stage('DeployStaging') {
      when {
        expression {
          action.startsWith("staging")
        }
      }
      steps {
        echo 'Deploying to Staging...'
      }
    }

    // DEPLOY TO PRODUCTION
    stage('DeployProduction') {
      when {
        expression {
          action.startsWith("production")
        }
      }
      steps {
        echo 'Deploying to Production...'
        echo App.getTarget(action)
      }
    }

  }
}



/*
stage('StagOneNG') {
  stages {
    // One or more stages need to be included within the stages block.
  }

  input {
    message 'Staging One NG'
  }

  environment {
    APP = "ci-app"
    LINUX = "debian"
  }

  options {
    checkoutToSubdirectory './temprepo'
    timestamps
  }

  when {
    branch 'dev'
    beforeAgent true
  }

  tools {
    git 'Default'
  }

  post {
    success {
      // One or more steps need to be included within each condition's block.
    }
  }
}
*/


// ver: https://jenkins.io/doc/book/pipeline/syntax/#stage

