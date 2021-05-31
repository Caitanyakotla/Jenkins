pipeline {
  environment {
    imagename = "caitanyakotla/udacitykrishnaprod"
    registryCredential = 'dockerhub-id'
    dockerImage = docker.build registry + ":$BUILD_NUMBER"
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
      git([url: 'https://github.com/Caitanyakotla/Jenkins.git', branch: 'master', credentialsId: '9786badb-5ab1-4adf-8e0b-dfe4c7cbfd02'])
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
