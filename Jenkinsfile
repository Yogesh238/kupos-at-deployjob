pipeline {
    agent any
    parameters {
        string(defaultValue: '', description: 'Enter Environment Name:', name: 'environment_name', trim: false)
        string(defaultValue: 'latest', description: 'Enter BUILD NUMBER to deploy [Default Value: latest]:', name: 'input', trim: false)
    }
 stages {
     stage('Pull file from S3 ') {
            steps {
                sh 'aws s3 cp s3://kupos-at-project/${input}.zip .'
            }
        }      
     stage("Deploy"){
           steps{
                script {
                    if (${environment_name} == 'master') {
                        echo 'I only execute on the master branch'
                    } else {
                        echo 'I execute elsewhere'
                    }
                 }              
              } 
          }
     }
}
