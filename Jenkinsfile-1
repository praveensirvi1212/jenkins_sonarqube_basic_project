pipeline {
    agent any
    tools { 
        maven 'maven-3.8.6' 
    }
    stages {
        stage('Checkout git') {
            steps {
               git branch: 'main', url: 'https://github.com/praveensirvi1212/jenkins_sonarqube_basic_project'
            }
        }
        
        stage ('Build & JUnit Test') {
            steps {
                sh 'mvn install' 
            }
            post {
               success {
                    junit 'target/surefire-reports/**/*.xml'
                }   
            }
        }
        stage('SonarQube Analysis'){
            steps{
                   withSonarQubeEnv('sonarqube') {
                        sh 'mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=devops-project-key \
                        -Dsonar.host.url=$sonarurl \
                        -Dsonar.login=$sonarlogin'
                    }
            }
        }
        stage('Deploy'){
            steps{
                sh 'timeout 60s java -jar /var/lib/jenkins/workspace/devopscicd/target/demo-0.0.1-SNAPSHOT.jar'
            }
        }
        }
    }
        
