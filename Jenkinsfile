properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		git credentialsId: 'github-credential', url: 'https://github.com/moumita12/java-project.git'
		sh 'ant -f test.xml -v'   
		junit 'reports/result.xml'
	}   
	stage('Build') {  
		sh 'ant -f build.xml -v'
	} 
	stage('Deploy') {    
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
		{
		sh 'aws s3 mb s3://assignment9-bucket'
		}
		sh 'aws s3 cp “/workspace/java-pipeline/dist/rect*.jar” s3://assignment9-bucket/'
	}
	stage('Report') {    
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
		{
                sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'  
                }
		
	}
}
