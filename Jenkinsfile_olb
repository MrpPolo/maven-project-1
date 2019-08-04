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
            post {
                success {
                    echo '开始存档...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy-to-stage'){
            steps{
                build job:'deploy-to-stagging'
            }
        }
        stage('Deploy-to-production'){
            steps{
                timeout(time:5,unit:'DAYS'){
                    input message:'是否deploy to production'
                }
                build job:'deploy-to-production'
            }
            post {
                success {
                    echo 'success...'
                }
                failure {
                    echo 'failure...'
                }
            }
        }
    }
}