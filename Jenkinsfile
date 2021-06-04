pipeline {
    agent any
    parameters {
        string(defaultValue: '', description: 'Enter Environment Name (Available Environments: dev & prod) :', name: 'environment', trim: false)
        string(defaultValue: 'latest', description: 'Enter BUILD NUMBER to deploy [Default Value: latest]:', name: 'input', trim: false)
    }
 stages {
     stage('Pull from Artifactory') {
            steps {
                sh 'aws s3 cp s3://kupos-at-project/${input}.zip .'
            }
        }      
     stage("Deploy"){
             steps{
                 sshagent(credentials : ['app_server']) {
                    if ( params.environment=='prod') {
                        sh 'scp ${input}.zip ubuntu@3.87.185.160:/root/go/go-web'
                    }
                     else if ( params.environment=='stage') {
                         sh 'scp ${input}.zip ubuntu@3.87.185.160:/root/go/go-stage'
                     }
                     
                       }
                    }
                }
//           steps{
//                script {
//                     if ( params.environment=='prod') {
//                         sh 'cp ${input}.zip /home/ec2-user/prod_environment'
//                         sh 'unzip -o /home/ec2-user/prod_environment/${input}.zip'
//                     } else if ( params.environment=='stage') {
//                         sh 'cp ${input}.zip /home/ec2-user/dev_environment'
//                         sh 'unzip -o /home/ec2-user/dev_environment/${input}.zip'
//                         sh 'rm /home/ec2-user/dev_environment/${input}.zip'
//                     }
//                  }              
//               } 
          
     }
}
