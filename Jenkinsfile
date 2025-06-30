pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/arvind37/Basic-Website-using-HTML-CSS.git'
        BRANCH = 'master'
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
                sudo apt upgrade -y

                sudo apt install nginx -y

                sudo rm -rf ${HTML_DIR}/*
                sudo cp -r * ${HTML_DIR}/
                sudo systemctl restart nginx
            '''
            }
        }
    }
}