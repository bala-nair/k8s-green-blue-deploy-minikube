node {
    def registry = 'bnair75/capstone-test'
    stage('Checking out git repo') {
      echo 'Checkout...'
      dir('subDir')
      checkout scm
    }
    stage('Checking environment') {
      echo 'Checking environment...'
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
    }
    stage("Linting") {
      echo 'Linting...'
      sh '/usr/bin/hlint Dockerfile'
    }
}
