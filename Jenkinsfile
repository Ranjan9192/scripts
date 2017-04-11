node {
   def mvnHome
   def javaHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git (url: 'https://github.com/mahendra-shinde/ci-demo2.git', credentialId: 'git-id')
      // Get the Maven tool.
      mvnHome = tool 'maven1'
      javaHome = tool 'jdk8'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
          sh "export JAVA_HOME=${javaHome}"
         sh "'${mvnHome}/bin/mvn' -f pom.xml  clean package"
      } else {
        bat (/"set JAVA_HOME=${javaHome}"/)
         bat(/"${mvnHome}\bin\mvn" -f pom.xml  clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}