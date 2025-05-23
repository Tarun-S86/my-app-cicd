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
        // e.g. for Java/Maven:
        // sh 'mvn clean package'
        // or for Node:
        // sh 'npm install && npm run build'
      }
    }

    stage('3. Unit & Integration Tests') {
      steps {
        // e.g. sh 'mvn test' or sh 'npm test'
      }
      post {
        always { junit '**/target/surefire-reports/*.xml' }
      }
    }

    stage('4. Static Code Analysis') {
      steps {
        // e.g. with SonarQube:
        // withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
        //   sh 'sonar-scanner -Dsonar.login=$SONAR_TOKEN'
        // }
      }
    }

    stage('5. Security Scan') {
      steps {
        // e.g. OWASP Dependency-Check:
        // sh 'dependency-check --project my-app --scan .'
      }
    }

    stage('6. Deploy to Staging') {
      steps {
        // e.g. sh 'docker build -t my-app:${GIT_COMMIT} .'
        //     sh 'docker push myregistry/my-app:${GIT_COMMIT}'
      }
    }

    stage('7. Integration Tests on Staging') {
      steps {
        // e.g. sh 'newman run tests/staging-collection.json'
      }
    }
  }

  post {
    success {
      echo '✅ Pipeline succeeded'
    }
    failure {
      mail to: 'dev-team@example.com',
           subject: "❌ Build failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "See ${env.BUILD_URL}"
    }
  }
}
