

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
    
        sh "chmod 777 ./ProcessingStage.sh"
       sh "./ProcessingStage.sh"
   }
 

   stage('Build') {
      // Run the maven build
        sh "sleep 5"
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
stage('Running Tests') {
    parallel JUnit: {
        echo 'Junit Test'
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test"
           sh "sleep 5"

    },
    DBTest: {
        echo 'DB Test'
           sh "sleep 5"

        },
     Jasmine: {
        echo 'Jasmine Test'
    sh "sleep 5"
    
    }
}

     stage('Code Coverage') {
                          echo 'Checking for Code Coverage'
    sh "sleep 5"

                        }

 
   stage('Artifacts') {
     
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
    sh "sleep 5"

   }
     stage('JUnit Report') {
                          echo 'Preparing JUnit Reports'
    sh "sleep 5"

                        }

   stage('Deploy App'){
   echo 'Deploying Application'
    sh "sleep 5"

   }
}

