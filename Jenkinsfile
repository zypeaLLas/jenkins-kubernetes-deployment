pipeline {

  environment {
    dockerimagename = "killua214/helloreppo"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git credentialsId: 'github-credentials',
			url: 'https://github.com/zypeaLLas/jenkins-kubernetes-deployment.git',
            branch: 'main'  // Đảm bảo tên branch đúng
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    

  }

}
