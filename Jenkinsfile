pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'mvn -B -DskipTests clean package'
          }
        }

        stage('Documentation') {
          steps {
            sh 'mvn site'
          }
        }

      }
    }

    stage('Test0') {
      parallel {
        stage('Test') {
          post {
            always {
              junit 'target/surefire-reports/*.xml'
            }

          }
          steps {
            sh 'mvn test'
          }
        }

        stage('Test1') {
          steps {
            sh 'mvn -Dtest=App getMessage test'
          }
        }

        stage('Test2') {
          steps {
            sh ' mvn -Dtest=AppTest testAppMain test'
            junit 'build/reports/**/*.xml'
          }
        }

      }
    }

    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
      }
    }

  }
  options {
    skipStagesAfterUnstable()
  }
}