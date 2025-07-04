pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/animesh-tyagi/jenkins-test.git'
        BRANCH = 'main'
        HTML_DIR = '/var/www/html'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: "${GIT_REPO}", branch: "${BRANCH}"
            }
            
        }
        stage('Build website') {
            steps {
                echo 'Starting server...'
            sh '''
                sudo apt update

                echo "Installing docker..."
                echo "Installing required packages..."
                sudo apt install -y ca-certificates curl gnupg

                echo "Adding docker GPG keys..."
                sudo install -m 0755 -d /etc/apt/keyrings

                curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor | sudo tee /etc/apt/keyrings/docker.gpg > /dev/null

                echo "Adding docker's apt repository..."
                echo \
                "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
                https://download.docker.com/linux/debian bookworm stable" | \
                sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

                sudo apt update
                sudo apt install -y docker-ce docker-ce-cli containerd.io

                
                echo "Containerizing application..."
                sudo docker build -t "nginx-server-image" .

                sudo docker rm -f nginx-server || true
                sudo docker run -d --name nginx-server -p 80:80 nginx-server-image

            '''
            }
        }
    }
}
