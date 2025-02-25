pipeline {
    agent any
    tools {
       maven "Maven 3.8.4"
   }

    stages {
        stage('1.Clone') {
            steps {
                echo 'clonning the latest version of the code..'
		git credentialsId: 'ada84d69-bfca-47b8-ba86-64e5dde5a754', url: 'https://github.com/TKC-PROJECT/spring-boot-docker'
            }
        }
        stage('2.Build') {
            steps {
                echo 'validation, compilation, testing and package..'
		echo 'testing successful and ready to package..'
		sh "mvn clean package" 		   
            }
        }
	stage('3.Quality') {
            steps {
                echo 'performing code quality analysis..'
		echo 'code quality successful and ready to upload..'
		sh "mvn sonar:sonar" 	
	    }
        }
	stage('4.UploadArtifacts') {
            steps {
                echo 'echo performing backup of build Artifacts..'
		sh "mvn deploy" 	
	    }
        }    
	stage('5.Build Docker Image') {
            steps {
		sh "docker build -t tikuodijie/ose ." 	
	    }
        }  
	stage('6.Push Docker Image') {
            steps {
		withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                 sh "docker login -u tikuodijie -p ${dockerhub}"
                }
		sh "docker push tikuodijie/ose"

	    }
        }  
	stage('7.RemoveDockerImages') {
            steps {
		sh 'docker rmi $(docker images -q)'	
	    }
        }        
        stage('8.Deploy To Kuberates Cluster') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
