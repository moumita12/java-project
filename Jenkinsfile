properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		git credentialsId: 'github-credential', url: 'https://github.com/moumita12/java-project.git'
		sh 'ant -buildfile test.xml'   
	}   
	stage('Build') {    
		sh 'ant'  
		//sh 'ant -f build.xml -v'
	}   
	stage('Results') {    
		//junit 'reports/*.xml'   
	}
}
