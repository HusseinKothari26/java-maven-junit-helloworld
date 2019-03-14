

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
      sleep 10000
   }
 

   stage('Build') {
      // Run the maven build
      sleep 10000
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
    },
    DBTest: {
        echo 'DB Test'
       sleep 10000
    },
     Jasmine: {
        echo 'Jasmine Test'
        sleep 10000
    }
}

     stage('Code Coverage') {
                          echo 'Checking for Code Coverage'
        sleep 10000
                        }

 
   stage('Artifacts') {
     
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      sleep 10000
   }
     stage('JUnit Report') {
                          echo 'Preparing JUnit Reports'
        sleep 10000
                        }

   stage('Deploy App'){
   echo 'Deploying Application'
      sleep 10000
   }
}

