pipeline {
    agent any
    parameters {
        string(defaultValue: '', description: 'Enter BUILD NUMBER to deploy', name: 'input', trim: false)
    }
 stages {
     stage("Deploy"){
           steps{
              sh "cp -r /root/.jenkins/workspace/Kupos_AT/img/${input}.png /home/ec2-user/apache-tomcat-8.5.66/webapps"
              } 
          }
     }
}
