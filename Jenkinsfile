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
                     script {
                     if ( params.environment=='prod') {
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.87.185.160 systemctl stop goweb.service'
                        sh 'scp ${input}.zip ubuntu@3.87.185.160:/root/go/go-web'
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.87.185.160 systemctl start goweb.service'
                    }
                     else if ( params.environment=='stage') {
                         sh 'ssh -v -o StrictHostKeyChecking=no ubuntu@3.87.185.160 systemctl stop gostage.service'
                         sh 'scp ${input}.zip ubuntu@3.87.185.160:/root/go/go-stage'
                         sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.87.185.160 systemctl start gostage.service'
                         sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.87.185.160 unzip -y /root/go/go-stage/${input}.zip'
                                }
                            }
                        }
                    }
                }
      stage('Infra Sanity Check') {
            steps {
                script{
                    status="\$(curl -Is http://3.87.185.160/ | head -1)"
                    validate=( $status )
                    if [ ${validate[-2]} == "200" ]; then
                      echo "Everything is Ok"
                    else
                      echo "NOT RESPONDING"
                    fi
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
