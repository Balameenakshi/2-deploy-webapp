pipeline {

agent { label 'master' }

	tools 
	{ 
	maven "M2_HOME"
	jdk "jdk 1.8"
	}

stages {
	stage("cloning from git")
	{
	steps { git credentialsId: 'Maven-Jar', url: 'https://github.com/Balameenakshi/2-deploy-webapp.git' }
	}

	stage("Build using Maven")
	{
	steps { 
	bat(/"%M2_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/) }
	}

	stage("Results")
	{
	steps { archiveArtifacts 'target/*.war' 
	deploy adapters: [tomcat8(credentialsId: 'd7b6d45b-dd3b-4cb4-9155-923e305f5308', path: '', url: 'http://localhost:8087')], contextPath: null, war: '**/*.war'
	}
	}
}

}
