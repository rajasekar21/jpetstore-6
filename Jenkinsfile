pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'first jenkins pipeline'
        sh 'mvn clean compile'
      }
    }

    stage('Unit Test') {
      steps {
        sh 'mvn test'
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('Static Analysis') {
      agent {
        node {
          label 'test'
        }

      }
      steps {
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Jpetstore \\
  -Dsonar.host.url=http://3.110.235.71:9000 \\
  -Dsonar.login=sqp_e98187d09a902049d01c2da3158b4ce1293b3565'''
      }
    }

    stage('Package') {
      agent {
        node {
          label 'test'
        }

      }
      steps {
        sh 'mvn package -DskipTests=true'
      }
    }

    stage('Integration Test') {
      agent {
        node {
          label 'test'
        }

      }
      steps {
        sh 'mvn verify -P tomcat90'
      }
    }

  }
}