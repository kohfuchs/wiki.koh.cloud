pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'mkdocs build'
      }
    }

    stage('deploy') {
      steps {
        sh 'rsync -av --delete site/ /var/www/wiki/'
      }
    }

    stage('cleanup') {
      steps {
        sh 'rm -rf site'
      }
    }

  }
  environment {
    CI = ''
  }
}