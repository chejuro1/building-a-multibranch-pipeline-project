pipeline {
  agent {
  docker {
    args 'args \'-p 3001:3000 -p 5001:5000\''
    customWorkspace '\\home\\ubuntu'
    image 'jenkinsci/jnlp-slave'
    label 'dev'
  }
}
stage('Build') {
  steps {
   sh 'npm install'
  }
}
}
