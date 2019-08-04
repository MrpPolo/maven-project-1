pipeline {
    agent any

    tools{
        maven 'local maven'
    }

    stages{
        stage('Init'){
            steps {
                echo "Testing......"
            }
        }
        stage('Build'){
                steps {
                    sh 'mvn clean package'
                }
            }
        stage('Deploy'){
                steps {
                    echo "Code Deployed."
                }
            }
        }
}