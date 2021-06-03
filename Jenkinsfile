pipeline {
    agent any
    parameters {
        text(name: 'input', defaultValue: '' , description: 'Enter BUILD NUMBER which you want to deploy (Number must be an integer)')
    }
 stages {
     stage("Deploy"){
           steps{
              sh "cp -r /root/.jenkins/workspace/Kupos_AT/img/${BUILD_NUMBER}.png /home/ec2-user/apache-tomcat-8.5.66/webapps"
              } 
          }
     }
}
