pipeline {
agent {label 'slavem1'}
triggers {
        pollSCM '* * * * *'
}
    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'ac9b9b85-f959-4234-b4b0-83fbccea7c4b', url: 'https://github.com/akkyaws/mavenrepo.git']]])
            }
        }
        stage('build'){
            steps{
                sh 'mvn package'
            }
        }
               stage('sonar'){
            steps{
                withSonarQubeEnv('mysonar'){ 
                sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('nexus'){
            steps{
            sh 'mvn deploy'
            }
        }
        
        stage('tomcat'){
            steps{
            sh 'scp /root/workspace/sample/target/studentapp-2.5-SNAPSHOT.war 54.251.167.45:/var/lib/tomcat/webapps'
            }
        }
              
    }
}
