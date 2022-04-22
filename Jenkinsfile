$ cat Jenkinsfile
pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/Josoungyun/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t starjo5/testweb:newnewmain .
        sudo docker push starjo5/testweb:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
	sudo kubectl set image deployment  deploy-main ctn-main=starjo5/testweb:newnewmain
        '''
      }
    }
  }
}
