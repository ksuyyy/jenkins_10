pipeline {
    agent any
environment{
    PATH= "/opt/maven/bin:$PATH"
}
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId:'github', url:'https://github.com/MonikaTrajkovska/hello-world.git'
            }
        }
        
        stage("deploy-dev"){
           steps{
               sshagent(['']) {
    sh """
    scp -o StrictHostKeyChecking=no webapp.war ec2-user@172.31.1.101:/opt/tomcat/webapps/
    ssh ec2-user@172.31.1.101 /opt/tomcat/bin/shutdown.sh
    ssh ec2-user@172.31.1.101 /opt/tomcat/bin/startup.sh
    """
           }
} 
        }
    }
}