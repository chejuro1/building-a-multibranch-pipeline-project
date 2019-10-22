pipeline {
    agent {
        docker {
            image 'jenkins-data:/var/jenkins_home'
            args '-p 3001:3000 -p 5001:5000'
            label 'dev'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }

agent {
  docker {
     args '-p 3002:3000 -p 5002:5000'
    customWorkspace '\\home\\ubuntu'
    image 'jenkinsci/jnlp-slave'
    label 'prod'
    registryCredentialsId 'chejuro'
    registryUrl 'https://hub.docker.com'
  }
}
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? 
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
