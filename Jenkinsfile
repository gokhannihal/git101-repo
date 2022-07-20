def commandMfront(var, command) {
    sh """
        if [ "${var}" == true ]; then ssh ubuntu@10.120.97.156 'cd /var/www/m-front;${command}' || exit 1; fi
    """
}

pipeline {
    agent any
    environment {
     gitCheckuothCommand = "git checkout ${branchname}"
    }
    stages {
        stage('preprod-Mfront') {
            steps {
                echo "branch name= ${branchname}" 
                echo "${gitCheckuothCommand}"
                commandMfront(true, 'git reset --hard')
                commandMfront(true, "git checkout ${branchname}")
                commandMfront(true, 'git pull')
                commandMfront(true, 'npm run build')
                commandMfront(true, 'pm2 restart 0')
                
            }
        }
    }
}
