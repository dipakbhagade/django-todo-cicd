pipeline {
   agent {label 'Django-Agent'}
     stages{
	   stage('code'){
	     steps{
		   echo "coding part"
		   git url:'https://github.com/dipakbhagade/django-todo-cicd.git', branch:'develop'
		   }
        }
        stage('build and test'){
	     steps{
		   echo "build and test"
		   sh 'docker build . -t dipak1994/django-todo:latest'
		   }
        }
        stage('push images to docker'){
	     steps{
		   echo "push images to docker"
		   withCredentials([usernamePassword(credentialsId:'docker-id', passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]){
		   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
		   sh 'docker push dipak1994/django-todo:latest'
		   }
		   }
        }
        stage('Deploy'){
	     steps{
		   echo "Deploy"
		   sh "docker-compose down && docker-compose up -d"
		   }
        }
	}
}
