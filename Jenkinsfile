pipeline {
    agent any
    parameters {
        string(defaultValue: '', description: 'Enter Environment Name:', name: 'Environment_name', trim: false)
        string(defaultValue: 'latest', description: 'Enter BUILD NUMBER to deploy [Default Value: latest]:', name: 'input', trim: false)
    }
 stages {
     stage('Pull file from S3 ') {
            steps {
                sh 'aws s3 cp s3://bucket/folder/${input}.zip .'
            }
        }      
     stage("Deploy"){
           steps{
              echo "yes"
              } 
          }
     }
}
