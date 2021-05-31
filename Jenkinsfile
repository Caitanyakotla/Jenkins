pipeline {
  environment {
    imagename = "caitanyakotla/udacitykrishnaprod"
    registryCredential = 'dockerhub-id'
    dockerImage = ''
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
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
  }
}
