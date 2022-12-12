
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

stage("Version Input"){
	input{
	massage "Enter the Build version"
	ok "Submit"
	parameters{
	string(name: 'IMAGEVERSION', defaultValue: 'V-0', trim: true)

	}
	}
	}

    
stage("build package"){
    steps{
    sh 'mvn -B -DskipTests clean package'
    }
    }

stage("Build Image"){
	steps{
	sh 'docker build $IMAGENAME:$IMAGEVERSION .'
	}
	}

stage("login to GitHub"){
	steps{
	sh 'echo $GitHub_Cred_PWD | docker login ghcr.io -u $GitHub_Cred_USR --password-stgin'
	}
	}
stage("Tag Image"){
	steps{
	sh 'docker tag $IMAGENAME:$IMAGEVERSION ghcr.io:/$IMAGENAME:$IMAGEVERSION'
	}
	}
stage("Push Image"){
	Steps{
	sh 'docker psuh ghcr.io:/$IMAGENAME:$IMAGEVERSION'
	}
	}

}
}
