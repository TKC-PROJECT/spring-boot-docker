pipeline {
   agent any

   tools {
       maven "Maven 3.8.4"
   }

   stages {
	     stage('1.Clone') {
		       steps{
			        sh "echo clonning the latest version of the code"
			        git credentialsId: 'ada84d69-bfca-47b8-ba86-64e5dde5a754', url: 'https://github.com/TKC-PROJECT/spring-boot-docker'
              sh "echo clonning successful"
		    }       
    }
 }
