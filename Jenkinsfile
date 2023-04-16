node("jenkins_slave") {
 	// Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
        	sh "echo 'clone scripts'"
		sh "git clone https://github.com/Ajithkumar48/Jenkins.git"
		sh ""
        }
        stage ('Build') {
        	sh "echo 'shell scripts to build project...'"
		sh "apt-get update"
		sh "sudo apt-get install ca-certificates curl gnupg"
		sh "sudo install -m 0755 -d /etc/apt/keyrings"
		sh "curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg"
		sh "sudo chmod a+r /etc/apt/keyrings/docker.gpg"
		sh "sudo apt-get update"
		sh "sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin"
		sh "sudo docker run hello-world"
		
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
