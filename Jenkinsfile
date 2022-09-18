pipeline{
    agent any
    environment{
        IMAGE_NAME = "mar97/php-project:1.0"
    }
    stages{
        stage("deployment"){
            steps{
                script{
                    echo "========executing A========"
                    def bashCmd ="bash ./cmd-server.sh ${IMAGE_NAME}"
                    def AWSCred = "ec2-user@3.144.116.160"
                    sshagent(credentials: ['ec2-docker-server']) {
                        
                        sh "ssh -o StrictHostKeyChecking=no ${AWSCred} docker run redis"

                    }
                }
            }
            post{
                success{
                    echo "========A deployment successfully========"
                }
                failure{
                    echo "========A deployment failed========"
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}