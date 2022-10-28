pipeline {
  agent any 
  stages {
    stage('git clone os git pull') {
      steps {
        git url: 'https://github.com/kimheeru/test2.git', branch: 'master'
      }
    }

    stage('docker image build and push t0 p-regiistry') {
      step {
	sh '''
        docker build -t 192.168.8.100:5000/testweb:blue .
        docker pull 192.168.8.100:5000/testweb:blue
        '''
      }
    }

    stage('deployment, svc creation') {
      steps { 
        sh '''
        kubectl create deploy testweb --image=192.168.8.100:5000/testweb:blue
        kubectl expose deploy testweb --type=LoadBalancer --port=80 --target-port=80 --name=testweb-svc
	'''
    }
  }
}
