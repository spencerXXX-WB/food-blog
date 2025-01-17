pipeline {
    agent {
     label 'WorkerNode1'
      }
    tools {
    maven 'maven'
    jdk 'jdk 20'
     }

    stages {
       
        stage('Compile') {
            steps {
                sh " mvn compile"
            }
        }
        stage('Test') {
            steps {
                sh " mvn test"
            }
        }
        stage('Package') {
            steps {
                sh " mvn package"
            }
        }
    }
     post {
  success {
      echo " Success"
     }
   }
}
