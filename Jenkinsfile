def bucket = 'xybersolve.io'
def build_dir = '/Users/Greg/Sites/gmilligan.github.io'

pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Web') {
      steps {
        sh 'make build-web'
      }
    }

    stage('Tag Web') {
      steps {
        sh 'make tag-web'
      }
    }

    stage('Push Web') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'pass', usernameVariable: 'user')]) {
          sh "make login user=${user} pass=${pass}"
          sh 'make push-web'
        }
      }
    }
  }
}

/*
node {

  stage('Checkout') {
    checkout scm
  }

  stage('Build') {
    sh 'make build-build'
  }

  stage('Build Web') {
    sh 'make build-web'
  }

  stage('Tag Web') {
    sh 'make tag-web'
  }
  stage('Push Web') {
    sh 'make login'
    sh 'make push-web'
  }

  stage('Push Web') {
    steps {
      withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'pass', usernameVariable: 'user')]) {
        echo "user: ${env.user}"
        echo "pass: ${env.pass}"
      }
    }
  }

  stage('Push Web') {
    // Jenkins withCredentials and make
    withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
      echo "user=${env.dockerHubUser}, pass=${env.dockerHubPassword}"
      //sh "make login user=${env.dockerHubUser} pass=${env.dockerHubPassword}"
      //sh 'make push-web'
      }
  }
}
*/
