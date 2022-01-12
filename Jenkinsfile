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
                         git 'https://github.com/intelliqittrainings/maven.git'
                    }
                    catch(Exception e1)
                    {
                      mail bcc: '', body: 'Jenkins is unable to download dev code from github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.team@gmail.com'
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
                         sh label: '', script: 'mvn package'
                    }
                    catch(Exception e2)
                    {
                       mail bcc: '', body: 'Jenkins is unable to create an artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'dev.team@gmail.com'
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
                         deploy adapters: [tomcat9(credentialsId: 'c8b5cc8f-c48f-4be4-9135-1028e410f38a', path: '', url: 'http://172.31.25.56:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on Qaservers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
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
                        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh label: '', script: 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium test scripts are failing', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
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
                        deploy adapters: [tomcat9(credentialsId: 'c8b5cc8f-c48f-4be4-9135-1028e410f38a', path: '', url: 'http://172.31.18.165:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the prodservers', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'
                    }
                }
                
            }
        }
    }
       
    }
