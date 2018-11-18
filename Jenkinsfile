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
		//junit 'reports/*.xml'   
	}
	stage('Report') {    
		//junit 'reports/*.xml'   
	}
}
