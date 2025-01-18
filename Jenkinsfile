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
                           $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=bloggingApp -Dsonar.projectKey=bloggingApp -Dsonar.Java.Binaries=target -Dsonar.branch.name=main 
                       '''
                   
                     sh "echo $SCANNER_HOME"
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
