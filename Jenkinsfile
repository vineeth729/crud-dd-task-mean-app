pipeline {
  agent any

  environment {
    DOCKERHUB_USER = 'vineeth837'                              // replace if different
    DOCKERHUB_CRED = 'dockerhub-credentials-id'               // Jenkins credentials ID for DockerHub
    EC2_HOST = 'ubuntu@54.208.240.43'                       // replace with your EC2 user@ip
    EC2_SSH_CRED = 'ec2-ssh-key-id'                           // Jenkins credentials ID (SSH private key)
    REPO = 'https://github.com/vineeth729/crud-dd-task-mean-app.git'
  }

  stages {
    stage('Checkout') {
      steps {
        git url: "${REPO}", branch: 'main'
      }
    }

    stage('Build Backend') {
      steps {
        dir('backend') {
          sh 'docker build -t ${DOCKERHUB_USER}/mean-backend:latest .'
        }
      }
    }

    stage('Build Frontend') {
      steps {
        dir('frontend') {
          sh 'docker build -t ${DOCKERHUB_USER}/mean-frontend:latest .'
        }
      }
    }

    stage('Login & Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKERHUB_CRED}", usernameVariable: 'DH_USER', passwordVariable: 'DH_PASS')]) {
          sh 'echo $DH_PASS | docker login -u $DH_USER --password-stdin'
          sh 'docker push ${DOCKERHUB_USER}/mean-backend:latest'
          sh 'docker push ${DOCKERHUB_USER}/mean-frontend:latest'
        }
      }
    }

    stage('Deploy to EC2') {
      steps {
        sshagent (credentials: ["${EC2_SSH_CRED}"]) {
          sh """
            ssh -o StrictHostKeyChecking=no ${EC2_HOST} '
              cd ~/apps/mean-crud || mkdir -p ~/apps/mean-crud && cd ~/apps/mean-crud
              # pull updated repo (optional) and ensure docker-compose file exists
              if [ -d .git ]; then git pull origin main || true; else git clone ${REPO} . || true; fi
              docker compose pull
              docker compose up -d
            '
          """
        }
      }
    }
  }

  post {
    success { echo 'Pipeline finished successfully' }
    failure { echo 'Pipeline failed' }
  }
}
