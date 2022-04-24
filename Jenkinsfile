pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''checkout
mkdir .pip_cache
cache restore
pip install --cache-dir .pip_cache -r requirements.txt
cache store'''
      }
    }

  }
}