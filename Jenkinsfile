
pipeline{
  
agent any
  
tools{
   maven "mvn" 
  
  }
  
environment{

GitHub_Cred=credentials('SharathBabuTR')
IMAGENAME='gcpbkash'
IMAGEVERSION='v1:latest'
	
}

stages{


stage("Build package"){

	steps{
	sh 'echo $IMAGEVERSION'
    sh 'mvn -B -DskipTests clean package'
    }
    }

stage("Build Image"){
	steps{
	sh "scp -r target/* /var/lib/jenkins/workspace/Fantasy_Test/Dockerfile/"
	sh 'sudo docker build -t $IMAGENAME/$IMAGEVERSION .'
	}
	}

stage("login to GitHub"){
	steps{
	sh 'echo $GitHub_Cred_PWD | sudo docker login ghcr.io -u $GitHub_Cred_USR --password-stgin'
	}
	}
stage("Tag Image"){
	steps{
	sh 'sudo dockr tag $IMAGENAME:$IMAGEVERSION ghcr.io:/$IMAGENAME/$IMAGEVERSION'
	}
	}
stage("Push Image"){
	steps{
	sh 'dockr push ghcr.io:/$IMAGENAME/$IMAGEVERSION'
	}
	}

}
}
