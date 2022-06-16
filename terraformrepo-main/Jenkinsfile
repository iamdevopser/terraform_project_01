pipeline{
  agent any

    environment {
        PASSWORD = credentials ('github_credential')
        AWS_ACCESS_KEY_ID=credentials("aws_access_key")
        AWS_SECRET_ACCESS_KEY=credentials("aws_secret_key")
  }  

    stages {

            stage('build Image'){
     
                    steps{
                        echo "Creating Image"
                        sh 'docker build . -t umutderman/jenkins:latest'
                    }
            }

             stage('Docker Push'){
     
                    steps{
                        echo "Pushing To DockerHub"
                        sh 'docker login -u umutderman -p ${PASSWORD}'
                        sh 'docker push umutderman/jenkins:latest'
                    }
            }

              stage('Create IS'){
     
                    steps{
                        echo "Creating InfraStructure"
                         sh """ 
                        #!/bin/bash
                        cd /var/jenkins_home/workspace/$JOB_NAME/
                        pwd
                        terraform init
                        terraform apply -auto-approve
                        """ 
                    }
                        
                    }
            }
    }

    