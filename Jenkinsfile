#!/usr/bin/env groovy

class App {
  String repo
  String repoBranch
  String repoKey
  String cfgStagBranch
  String cfgProdBranch
  String chartType
  String userAction

  static String getConfigRepo(String service = 'one') {
    'configs' + service
  }

  String helmStagingValuesFilename(String service, String country) {
    'staging-' + service + '-' + repo + '-' + country + '.yaml'
  }

  static String getTarget(String action) {
    String[] str = action.split('-')
    str[0]
  }

  static String getiService(String action) {
    String[] str = action.split('-')
    str[0]
  }

  static String getCountry(String action) {
    String[] str = action.split('-')
    str[0]
  }
    
    //for( String values : str )
    //  echo values

//    if (action.size == 3)
//      str[2]
//    else
//      'error'
}


staging-one-ng


String[] countries = ['ci', 'eg', 'ke', 'ma', 'ng']
String[] services = ['one', 'flights', 'jforce']
def app = new App(
                repo:           'daenerys',
                repoBranch:     'dev',
                repoKey:        '20e0cddc-61b3-40c3-a6bc-f630d210b518',
                cfgStagBranch:  'dev',
                cfgProdBranch:  'production',
                chartType:      'raw',
                userAction:     action
              )


def appMap = [:]
appMap.put('staging-one-ng', app)
appMap.put('staging-one-eg', app)

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
        echo app.userAction
        echo appMap.get(action)
        echo appMap.get(action).repo

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

