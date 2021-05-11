node
{
	def mavenHome = tool name: "maven3.8.1"
	stage('CheckoutCode')
	{
	 git branch: 'development', credentialsId: 'e5accc3f-5af6-4850-bcf8-4d8ff1f6fec8', url: 'https://github.com/mounika1896/maven-web-application.git'
	}
	
	stage('Build')
	{
	 sh "${mavenHome}/bin/mvn clean package"
	}
	
	stage('ExecuteSonarQubeReport')
	{
	 sh "${mavenHome}/bin/mvn sonar:sonar"
	}
	
	stage('UploadArtifactsIntoNexus')
	{
	 sh "${mavenHome}/bin/mvn deploy"
	}
	
	stage('DeployAppIntoTomcat')
	{
	sshagent(['60c62c92-75a8-40e8-83ca-268b45b96f1e'])
	 {
	   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@13.234.112.117:/opt/tomcat9/webapps/"
	 }
	}
/*	
	stage('SendEmailNotification')
	{
     mail bcc: '', body: '''Build Over..

Regards
Mounika Reddy
8500355951''', cc: 'mounikareddy3it@gmail.com', from: '', replyTo: '', subject: 'Build Over..', to: 'vennapusamounika9@gmail.com'
    }
*/   
}
