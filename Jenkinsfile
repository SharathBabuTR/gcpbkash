
pipeline{
  
agent any
  
tools{
   maven "mvn" 
  }
  
environment{

GitHub_Cred=credentials('SharathBabuTR')
IMAGENAME='gcpbkash'
	
}

stages{

stage("Inmput Version"){
	steps{
		script{
	def IMAGEVERSION=input ( message: 'Enter the Build version', ok: 'Submit', parameters: [string(name: 'ImageVersion',defaultValue: ' ',description: ' ')])
	
	echo '$IMAGEVERSION'
	}
	}	
}
stage("Build package"){

	steps{
	sh 'echo $IMAGEVERSION'
    sh 'mvn -B -DskipTests clean package'
    }
    }

stage("Build Image"){
	steps{
	sh 'docker build -t $IMAGENAME/$IMAGEVERSION .'
	}
	}

stage("login to GitHub"){
	steps{
	sh 'echo $GitHub_Cred_PWD | docker login ghcr.io -u $GitHub_Cred_USR --password-stgin'
	}
	}
stage("Tag Image"){
	steps{
	sh 'docker tag $IMAGENAME:$IMAGEVERSION ghcr.io:/$IMAGENAME/$IMAGEVERSION'
	}
	}
stage("Push Image"){
	steps{
	sh 'docker push ghcr.io:/$IMAGENAME/$IMAGEVERSION'
	}
	}

}
}
