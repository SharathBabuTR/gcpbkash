pipeline{
  
  agent any
  
  tools
  
  {
   maven "mvn" 
  }
  
  stages{

    
    stage("build")
    {
      steps{
      sh 'mvn -B -DskipTests clean package'
      }
    }
  
  }
  
}
