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
                        git 'https://github.com/selenium-saikrishna/maven.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to download the code from github.', cc: '', from: '', replyTo: '', subject: 'ContinuousDownload Failed', to: 'git.team@gmail.com'
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
                        mail bcc: '', body: 'Jenkins is unable to build an artifact from the code we downloaded from github.', cc: '', from: '', replyTo: '', subject: 'ContinuousBuild Failed', to: 'developer.team@gmail.com'
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
                        deploy adapters: [tomcat9(credentialsId: 'f011aa4f-2e7b-461e-b807-ce4fef55befd', path: '', url: 'http://172.31.99.172:8080')], contextPath: 'jackdepl', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Deployment into the tomcat of the QAServer has failed. Kindly check and advise.', cc: '', from: '', replyTo: '', subject: 'ContinuousDeployment Failed', to: 'middleware.team@gmail.com'
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
                        sh 'java -jar /var/lib/jenkins/workspace/TestDeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'jenkins is unable to test the selenium code from github. Kindly check and advise.', cc: '', from: '', replyTo: '', subject: 'ContinuousTesting Failed', to: 'qa.team@gmail.com'
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
                       input message: 'Waiting for approval from the DM !', submitter: 'anto'
                       deploy adapters: [tomcat9(credentialsId: 'f011aa4f-2e7b-461e-b807-ce4fef55befd', path: '', url: 'http://172.31.109.217:8080')], contextPath: 'deplene', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into the tomcat of the prodserver. Kindly check and advise.', cc: '', from: '', replyTo: '', subject: 'ContinuousDelivery Failed', to: 'delivery.team@gmail.com'
                    }
                }
            }
        }
    }
}
