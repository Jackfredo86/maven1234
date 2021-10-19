pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_Loans')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/Jackfredo86/maven1234.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to download the code from github.', cc: '', from: '', replyTo: '', subject: 'ContinuousDownload Failed', to: 'git.team@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild_Loans')
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
	
    }
}
     
