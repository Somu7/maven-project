pipeline {
    agent any

    stages {
        stage('Git Clone') {
            steps{
                git credentialsId: 'Git_credentials', url: 'https://github.com/Somu7/maven-project.git'
            }
        }
        stage('Maven Build') {
            steps {
                    sh "mvn  install"
                           echo "mvn install successfully"
                }
        }
        stage('Build docker image') {
            steps {
                sh'''
                docker rmi -f somu9491/mavenimg
                cd /var/lib/jenkins/workspace/pipeline
                docker build -t=somu9491/mavenimg .
                '''
            }
        }
         stage ('Push docker image to docker hub') {
            steps {
                withCredentials([string(credentialsId: 'Docker1_Hub_credentials', variable: 'Docker1_Hub_credentials')]) {
                sh "docker login -u somu9491 -p ${Docker1_Hub_credentials}"
                }
                sh " docker push somu9491/mavenimg "
            }
        }
     }
 }
