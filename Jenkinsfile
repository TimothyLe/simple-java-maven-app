pipeline {
  agent {
    label 'docker'    
  }
  stages {
    stage('Build') {
      agent {
        docker {
          label 'docker'  
          image 'maven:3-alpine'
          args '-v /root/.m2:/root/.m2'
        }
      }
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
  }
}
