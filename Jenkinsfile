pipeline {
  agent any

  options {
    timestamps()
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Setup Tooling') {
      steps {
        bat 'node -v'
        bat 'npm -v'
        bat 'where yarn || npm install -g yarn'
        bat 'yarn --version'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'yarn install'
      }
    }

    stage('Unit Tests') {
      steps {
        bat 'yarn run test'
      }
    }

    stage('E2E Tests') {
      steps {
        bat 'yarn run e2e'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'results.xml, reports/**', allowEmptyArchive: true
    }
  }
}
