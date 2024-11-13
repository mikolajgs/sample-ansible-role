pipeline {
    options {
      buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '1'))
      gitLabConnection("${GITLAB_CONNECTION_NAME}")
      disableConcurrentBuilds()
    }
    agent {
        docker {
          image 'some repo'
          args "-v /var/run/docker.sock:/var/run/docker.sock --group-add 998"
          alwaysPull true
        }
    }
    stages {
        stage('Test') {
            when {
                changeRequest()
            }
            steps {
                sh '''
                pip install -r requirements.txt
                molecule test
                '''
            }
        }
    }
}
