pipeline {
  agent {
    label 'auditjs-node'
  }
  stages {
    stage('Pull Source') {
      // Get some code from a GitHub repository
      steps {
        git url: 'https://github.com/bkimminich/juice-shop.git'
      }
    }
    stage('Build & Install') {
      steps {
        echo "Performing build"
        sh 'npm -v'
        sh 'npm install'
        sh 'npm pack'
      }
    }
    stage('Nexus Lifecycle Evaluation') {
      steps {
        sh 'auditjs iq -a ${JOB_BASE_NAME} -d --server ${IQserver} -u ${IQusername} -p ${IQpassword} -s build'
      }
    }
  }
}
