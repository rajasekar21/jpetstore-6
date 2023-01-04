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
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Jpetstore \\
  -Dsonar.host.url=http://3.110.235.71:9000 \\
  -Dsonar.login=sqp_e98187d09a902049d01c2da3158b4ce1293b3565'''
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package -DskipTests=true'
      }
    }

  }
}