node {
    def registry-blue = 'bnair75/capstone-blue'
    def registry-green = 'bnair75/capstone-green'
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
	     	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
	     	sh "docker build -t ${registry-blue} ."
	     	sh "docker tag ${registry-blue} ${registry-blue}"
	     	sh "docker push ${registry-blue}"
      }
    }
    stage('Building image green') {
	    echo 'Building Docker image green...'
      withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
	     	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
	     	sh "docker build -t ${registry-green} ."
	     	sh "docker tag ${registry-green} ${registry-green}"
	     	sh "docker push ${registry-green}"
      }
    }
}
