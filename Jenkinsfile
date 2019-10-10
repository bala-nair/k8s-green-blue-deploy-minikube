node {
    def registry1 = 'bnair75/capstone-blue'
    stage('Checking out git repo') {
      echo 'Checkout...'
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
      sh '/usr/bin/hlint blue/Dockerfile'
      sh '/usr/bin/hlint green/Dockerfile'
    }
    stage('Building image blue') {
	    echo 'Building Docker image blue...'
      withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
	     	sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
	     	sh "sudo docker build -t ${registry} blue/."
	     	sh "sudo docker tag ${registry} ${registry}"
	     	sh "sudo docker push ${registry}"
      }
    }
}
