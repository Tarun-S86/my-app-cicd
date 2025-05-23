pipeline {
  agent any

  stages {
    stage('1. Checkout') {
      steps {
        checkout scm
      }
    }

    stage('2. Build') {
      steps {
        echo '⏳ Building…'
        // e.g. sh 'npm install && npm run build'
      }
    }

    stage('3. Unit & Integration Tests') {
      steps {
        echo '🧪 Running tests…'
        // e.g. sh 'npm test'
      }
      post {
        always {
          // allowEmptyResults avoids failure if there are no XML reports
          junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
        }
      }
    }

    stage('4. Static Code Analysis') {
      steps {
        echo '🔍 Static analysis…'
        // e.g. withCredentials([...]) { sh 'sonar-scanner …' }
      }
    }

    stage('5. Security Scan') {
      steps {
        echo '🔒 Security scan…'
        // e.g. sh 'npm audit --audit-level=high'
      }
    }

    stage('6. Deploy to Staging') {
      steps {
        echo '🚀 Deploying to staging…'
        // e.g. sh 'docker build -t my-app:${GIT_COMMIT} .'
      }
    }

    stage('7. Integration Tests on Staging') {
      steps {
        echo '🔗 Running staging integration tests…'
        // e.g. sh 'newman run tests/staging-collection.json'
      }
    }
  }

  post {
    success {
      echo '✅ Pipeline completed successfully!'
    }
  }
}
