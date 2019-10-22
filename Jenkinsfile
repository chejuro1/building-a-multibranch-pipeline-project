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
agent {
  docker {
    args 'args \'-p 3002:3000 -p 5002:5000\''
    customWorkspace '\\home\\ubuntu'
    image 'jenkinsci/jnlp-slave'
    label 'prod'
  }
}
  
stage('Build') {
  steps {
    sh './jenkins/scripts/deliver-for-development.sh'
  }
}
}

