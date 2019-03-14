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
    
        sh "chmod 777 ./Stages/*"
       sh "./Stages/ProcessingStage.sh"
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

