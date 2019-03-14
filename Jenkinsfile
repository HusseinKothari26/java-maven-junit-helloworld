

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
      sleep 3000
   }
 

   stage('Build') {
      // Run the maven build
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
       sleep(time:10,unit:"SECONDS")
    },
     Jasmine: {
        echo 'Jasmine Test'
        sleep(time:5,unit:"SECONDS")
    }
}

     stage('Code Coverage') {
                          echo 'Checking for Code Coverage'
        sleep(time:7,unit:"SECONDS")
                        }

 
   stage('Artifacts') {
     
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      sleep(time:5,unit:"SECONDS")
   }
     stage('JUnit Report') {
                          echo 'Preparing JUnit Reports'
        sleep(time:6,unit:"SECONDS")
                        }

   stage('Deploy App'){
   echo 'Deploying Application'
      sleep(time:15,unit:"SECONDS")
   }
}

