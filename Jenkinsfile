pipeline{
    agent any

    parameters{
        string(name: 'tomcat_dev', defaultValue: '54.199.185.207', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: '54.199.185.207', description: 'Production Server')
    }

    triggers{
        pollSCM('* * * * *')
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

        stage ('Deployments'){
            sshagent(credentials: ['deploy_ssh_key'])
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                    }
                }

                // stage ("Deploy to Production"){
                //     steps {
                //         sh "scp **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
                //     }
                // }
            }
        }   
    }
}