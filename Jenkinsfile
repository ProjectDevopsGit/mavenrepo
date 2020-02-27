def tomcat = "18.218.233.17"
pipeline{
	agent { label 'qa' }
	stages{
		stage('checkout'){
			steps{
				checkout([$class: 'GitSCM', 
    branches: [[name: '*/qa']], 
    userRemoteConfigs: [[credentialsId: '75925fff-cc1c-42a0-b7fe-dedbe644d5c8', url:'https://github.com/ProjectDevopsGit/mavenrepo.git']]
])

			     }
					   }
		stage('build'){
			steps{
				sh "mvn package"
			
				 }
                    }
		stage('sonar'){
			steps{
			    withSonarQubeEnv('sonarqube'){
				sh "mvn sonar:sonar"
				
			    }
				
			      }
					   }
		stage('deploy'){
			steps{
			sh "ssh $tomcat systemctl stop tomcat"
			sh "scp target/*.war $tomcat:/var/lib/tomcat/webapps"	
			sh "ssh $tomcat systemctl start tomcat"
			}
		}
		
		  }
		}
