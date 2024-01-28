pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/MaorYahalomi/curriculum-app', branch: 'dev')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile -t maordockr89/nodeapp:latest .'
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKER_CREDENTIALS = credentials('docker-pass')
        DOCKERHUB_USER = 'maordockr89'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKER_CREDENTIALS"
      }
    }

    stage('Push') {
      steps {
        sh 'docker push maordockr89/nodeapp:latest'
      }
    }

  }
}
