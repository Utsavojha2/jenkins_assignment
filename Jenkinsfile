pipeline {
  agent any

  environment {
    // Set Node.js version path (if using nvm or system node)
    NODE_HOME = '/usr/bin'
    PATH = "${NODE_HOME}:${PATH}"
    BUILD_DIR = 'build'
    DEPLOY_DIR = '/var/www/reactapp'
  }

  stages {
    stage('Checkout') {
      steps {
        echo 'Cloning repository...'
        git branch: 'main', url: 'https://github.com/yourusername/your-react-app.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        echo 'Installing npm dependencies...'
        sh 'npm install'
      }
    }

    stage('Build React App') {
      steps {
        echo 'Building the React app...'
        sh 'npm run build'
      }
    }

    stage('Deploy to Nginx') {
      steps {
        echo 'Deploying to Nginx...'

        sh """
        sudo mkdir -p ${DEPLOY_DIR}
        sudo cp -r ${BUILD_DIR}/* ${DEPLOY_DIR}/
        """
      }
    }
  }

  post {
    success {
      echo 'Deployment completed'
    }
    failure {
      echo 'Deployment failed.'
    }
  }
}
