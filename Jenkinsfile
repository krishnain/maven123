pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                         git 'https://github.com/krishnain/maven.git'
                    }
                    catch(Exception e1)
                    {
                       mail bcc: '', body: 'Jenkins is unable to download the devlopment code from remote github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.admin@gmail.com'
                       exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                         sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                       mail bcc: '', body: 'Jenkins is unable to create an artifact from the code', cc: '', from: '', replyTo: '', subject: 'BuildFailed', to: 'dev.team@gmail.com'
                       exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                         deploy adapters: [tomcat9(credentialsId: '4b4c794d-8cc6-4379-b396-e9e771df80d4', path: '', url: 'http://172.31.90.45:8080')], contextPath: 'mytestapp', war: '**/*.war'
                         
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on QAServers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                         git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                         sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium scripts are failing', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                         
               deploy adapters: [tomcat9(credentialsId: '4b4c794d-8cc6-4379-b396-e9e771df80d4', path: '', url: 'http://172.31.95.150:8080')], contextPath: 'myprodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy  into tomcat on the prodservers', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'
                    }
                }
              
            }
        }
        
        
        
        
        
    }
}
