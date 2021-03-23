pipeline {
  agent { label "docker" }
  stages {
    stage("build") {
      steps {
        sh """
          docker build -t hello_there .
        """
      }
    }
    stage("run") {
      steps {
        sh """
          docker run --rm hello_there
        """
      }
    }
    stage("create a new docker container") {
      steps {
        sh """
          docker run -d -p 3000:3000 node:6-alpine
        """
      }
    }
  }
}
