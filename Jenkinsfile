pipeline{
    agent any
    
    stages{
    stage("Git checkout"){
        steps{
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/Dilliprasady/Ai-Leads.git'
        }
    }
     stage("Maven build"){
         steps{
             sh 'mvn clean package'
         }
        }
             stage("Tomcat deploy-dev"){
         steps{
             sshagent(['Tomact-dev']) {
              // copy war file to tomcat
              sh "scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.45.64:/opt/tomcat9/webapps"
              sh "ssh ec2-user@172.31.45.64 /opt/tomcat9/bin/shutdown.sh"
              sh "ssh ec2-user@172.31.45.64 /opt/tomcat9/bin/startup.sh"
            }
         }
       }
    }
}
