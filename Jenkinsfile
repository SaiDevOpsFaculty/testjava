pipeline{
    agent any
    stages{
        stage("git checkout"){
            steps{
              git 'https://github.com/sahooashok709/time-tracker.git'
            }
        }
        stage("build in maven"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("deploy in tomcat"){
            steps{
                sshagent(['tomcat']) {
                sh """
                   scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/new_pipeline/web/target/time-tracker-web-0.5.0-SNAPSHOT.war  ec2-user@172.31.10.239:/opt/tomcat8/webapps
                   ssh ec2-user@172.31.10.239 /opt/tomcat8/bin/shutdown.sh
                   ssh ec2-user@172.31.10.239 /opt/tomcat8/bin/startup.sh
                   """ 
                }
            }
        } 
      
    }
}
