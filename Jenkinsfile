pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/sainanivishal58/gitrepo2', branch: 'main')
      }
    }

    stage('Build&Push') {
      steps {
        sh '''sudo docker build-t sainanivishal58/srepo1:latest
sudo docker push sainanivishal58/srepo1:latest'''
      }
    }

    stage('DeployDev') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -p -d 7777:80 --name devcon1 sainanivishal58/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 sainanivishal58/srepo1:latest'''
          }
        }

      }
    }

  }
}