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
	sudo sed -i 's/USING/HIHI/g' index.html
        sudo docker build -t starjo5/testweb:newblog .
	sudo sed -i 's/USING/HELLO/g' index.html
	sudo docker build -t starjo5/testweb:newshop .
        sudo docker push starjo5/testweb:newblog
	sudo docker push starjo5/testweb:newshop
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
	sudo kubectl set image deployment deploy-blog ctn-blog=starjo5/testweb:newblog
	sudo kubectl set image deployment deploy-shop ctn-shop=starjo5/testweb:newshop
        '''
      }
    }
  }
}
