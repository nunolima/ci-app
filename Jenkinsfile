class App {
  String repo
  String key
  String serviceName
  String stagBranch
  String prodBranch

  def helmStagingValuesFilename() {
    'staging-' + repo + '-' + serviceName + '-' + repo + '.yaml'
  }

}

def app1 = new App(repo: 'mario', key: 'AS$I$A#RG%4923bnf#4r', stagBranch: 'dev', prodBranch: 'production')

def appOutput(String line = '---') {
  echo line
}

node {
  // STAGING
  stage('StagOneNG') {
    if (action in ["Build", "StagOneNG"]) {
      appOutput(app1.helmStagingValuesFilename())
    }
  }

  // PRODUCTION
  stage('ProdOneNG') {
    if (action in ["Build", "ProdOneNG"]) {
      appOutput()
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

