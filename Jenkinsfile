pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
               // slackSend channel: 'youtubejenkins', message: 'Job Started'
                
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn install"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
               // deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://192.168.0.118:8080')], contextPath: '/app', war: '**/*.war'
               deploy adapters: [tomcat9(credentialsId: 'tomcat2', path: '', url: 'http://http://3.110.155.98:8080')], contextPath: '/app', war: '**/*.war'
            }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container -> plugin
             deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://52.66.208.45:8080')], contextPath: '/app', war: '**/*.war'
echo "DEPLOY ON PROD"
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
           //  slackSend channel: 'youtubejenkins', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
          //   slackSend channel: 'youtubejenkins', message: 'Job Failed'
        }
    }
}
