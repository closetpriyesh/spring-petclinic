pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        echo 'Checking out!!'
        git 'https://github.com/closetpriyesh/spring-petclinic.git'
      }
    }

    stage('build') {
      parallel {
        stage('build') {
          steps {
            echo 'Building out!!'
            script {
              env.PATH = "C:/Users/Priyesh_Kumar/Downloads/apache-maven-3.6.3-bin/apache-maven-3.6.3/bin;c:\\Windows\\System32"
            }

            bat 'mvn package'
          }
        }

        stage('API_Test') {
          steps {
            echo 'Running API Tests'
          }
        }

      }
    }

    stage('archive') {
      steps {
        echo 'Archiving out!!'
        archiveArtifacts 'target/*.jar'
      }
    }

  }
  post {
    always {
      echo 'Pipeline finished'
      step([$class: 'JUnitResultArchiver', testResults: '/target/surefire-reports/*.xml'])
    }

  }
}