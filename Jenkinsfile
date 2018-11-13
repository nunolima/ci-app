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
