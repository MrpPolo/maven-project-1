pipeline {
    agent any

    tools{
        maven 'local maven'
    }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy-to-stage'){
            steps{
                build job:'deploy-to-stagging'
            }
        }
    }
}