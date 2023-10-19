pipeline{
 agent any
  stages{
   stage('Checkout Repo') {
    steps{
     checkout([$class: CheckOutClass, branches: [[name: BranchName]], browser: [$class: BrowserClass], userRemoteConfigs: [[credentialsId: PrivateKeyID, url: SourceURL]]])
    }
   }
   stage('Clean'){
    steps{
     dir(ApplicationPath) {
      sh '''
       mvn clean && echo Hi bharath
       if [ -f ${ArtifactsPath}/*.jar ]
       then
        rm ${ArtifactsPath}/*.jar
       else
        echo "no jar file"
       fi
       '''
     }
    }
   }
   stage('build'){
    steps{
     dir(ApplicationPath) {
      sh 'mvn package  -Dcustom.output.directory=${ArtifactsPath}'
     }
    }
   }
  }
 }
