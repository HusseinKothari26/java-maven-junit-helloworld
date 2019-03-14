node {
   def mvnHome
     stage('Clean WS'){
        cleanWs()
   }
   stage('SCM Checkout') { 
      // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/HusseinKothari26/java-maven-junit-helloworld.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
<<<<<<< HEAD
      sh "chmod 777 ./ProcessingStage.sh"
      sh "./ProcessingStage.sh"
=======
    
        sh "chmod 777 ./Stages/*"
       sh "./Stages/ProcessingStage.sh"
>>>>>>> 67238e6edbea38243064097f5e9f8af00a30d0f8
   }
 

   stage('Build Step') {
      // Run the maven build
        
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
       sh "./Stages/BuildChecks"
   }
stage('Running Tests') {
    parallel JUnit: {
        echo 'Junit Test'
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test"
           sh "./Stages/Junit"

    },
    DBTest: {
        echo 'DB Test'
            sh "./Stages/DBTest"

        },
     Jasmine: {
        echo 'Jasmine Test'
     sh "./Stages/DBTest"
    
    }
}

     stage('Code Coverage') {
                          echo 'Checking for Code Coverage'
     sh "./Stages/CodeCoverage"

                        }

 
   stage('Artifacts') {
     
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
 sh "./Stages/Artifact"

   }
     stage('JUnit Report') {
                          echo 'Preparing JUnit Reports'
     sh "./Stages/JunitReport"

                        }

   stage('Deploy App'){
   echo 'Deploying Application'
     sh "./Stages/Deploy"

   }
}

