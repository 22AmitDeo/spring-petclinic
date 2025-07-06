pipeline {
  agent any

  environment {
    IMAGE_NAME = "spring-petclinic"
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/<your-username>/spring-petclinic.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t $IMAGE_NAME:latest .'
      }
    }

    stage('Deploy') {
      steps {
        sh 'docker-compose down || true'
        sh 'docker-compose up -d'
      }
    }
  }
}
