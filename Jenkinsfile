pipeline {
    agent any

    stages {
        //stage('Git checkout') {
        //    steps {
        //        git 'https://github.com/faridaabdul/sonarqube-nexusRepo.git'
                git branch: 'main',url: 'https://github.com/faridaabdul/sonarqube-nexusRepo.git'
        //    }
        //}
        
        stage('Build with maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
        
             stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        
            }
        stage('Code Qualty Scan') {

           steps {
                  withSonarQubeEnv('sonar_server') {
             sh "mvn -f SampleWebApp/pom.xml sonar:sonar"      
               }
            }
       }
        stage('Quality Gate') {
          steps {
                 waitForQualityGate abortPipeline: true
              }
        }
            
        }
}  
 
