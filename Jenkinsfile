pipeline {
    agent any
    
    tools {
        maven 'maven'
        jdk 'jdk17'
     }
     environment {
        SCANNER_HOME= tool 'sonar-scanner'
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
        stage('Sonarqube Analysis') {
            steps {
                withSonarQubeEnv('sonarserver') {
                    sh ''' 
                           $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=bloggingApp1 -Dsonar.projectKey=bloggingApp1 -Dsonar.java.binaries=target
                       '''
                   
                     sh "echo $SCANNER_HOME"
            }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                 waitForQualityGate abortPipeline: false, credentialsId: 'SonarSecret'
            }
            }
        }
        
    }
     post {
  success {
      echo " Success"
     }
   }
}
