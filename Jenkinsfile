pipeline {
  agent { label "node1" }
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
          docker run -d --rm --name alpine -p 3000:3000 node:6-alpine
        """
      }
    }
    stage("Start the docker container alpine") {
      steps {
        sh """
          docker start alpine
        """
      }
    }
    stage {
      node('node1'){
        stage("Scan alpine image"){
          aqua locationType: 'local', localImage: 'alpine', hideBase: false, notCompliesCmd: '', onDisallowed: 'ignore', showNegligible: false
        }
      }
    }    
    stage("Stop and remove the docker container alpine") {
      steps {
        sh """
          docker rm -f alpine
        """
      }
    }        
  }
}
