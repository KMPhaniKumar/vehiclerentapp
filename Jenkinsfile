awscreds = 'ecr:us-east-1:awscreds'

// imagename for docker image tag name
imagename = "216666225420.dkr.ecr.us-east-1.amazonaws.com/rentalcars"



//This ecrRegistry is to push the docker image from jenkins to ECR
ecrRegistry = "https://216666225420.dkr.ecr.us-east-1.amazonaws.com"


node(){

   stage("Git Checkout"){
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'repo3git', url: 'https://github.com/KMPhaniKumar/vehiclerentapp.git']]])
   }
   
   stage("Maven Build"){
   sh "mvn clean install"
   }
   
   stage("Create Docker Image"){
   
   dockerImage = docker.build( imagename + ":$BUILD_NUMBER")
   
   }
   
   
   stage("Uplaod image to ECR"){
   
   docker.withRegistry( ecrRegistry, awscreds) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
          }
    
   
   }

