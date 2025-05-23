pipeline {
  agent any

  stages {
    stage('1. Checkout') {
      steps {
        // Pulls your code from the branch being built
        checkout scm
      }
    }

    stage('2. Build') {
      steps {
        echo 'Building…'
        // e.g. for Java/Maven:
        // sh 'mvn clean package'
        // or for Node.js:
        // sh 'npm install && npm run build'
      }
    }

    stage('3. Unit & Integration Tests') {
      steps {
        echo 'Running tests…'
        // sh 'mvn test'
        // or: sh 'npm test'
      }
      post {
        always {
          // Archives JUnit XML reports
          junit '**/target/surefire-reports/*.xml'
        }
      }
    }

    stage('4. Static Code Analysis') {
      steps {
        echo 'Static analysis…'
        // withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
        //   sh "sonar-scanner \
        //       -Dsonar.host.url=$SONAR_HOST_URL \
        //       -Dsonar.login=$SONAR_TOKEN"
        // }
      }
    }

    stage('5. Security Scan') {
      steps {
        echo 'Security scan…'
        // e.g. OWASP Dependency-Check:
        // sh 'dependency-check --project my-app --scan .'
        // or for Node:
        // sh 'npm audit --audit-level=high'
      }
    }

    stage('6. Deploy to Staging') {
      steps {
        echo 'Deploying to staging…'
        // sh 'docker build -t my-app:${GIT_COMMIT} .'
        // sh 'docker push myregistry/my-app:${GIT_COMMIT}'
        // then invoke your staging rollout (kubectl, Ansible, etc.)
      }
    }

    stage('7. Integration Tests on Staging') {
      steps {
        echo 'Running staging integration tests…'
        // sh 'newman run tests/staging-collection.json'
      }
    }
  }

  post {
    success {
      echo 'Pipeline completed successfully!'
    }
    failure {
      mail to: 'dev-team@example.com',
           subject: "Build failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Check the console output at ${env.BUILD_URL}"
    }
  }
}
