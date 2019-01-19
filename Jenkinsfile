node('maven-label') {
   def mvnHome
   stage('Preparation') { 
      
      git 'https://github.com/aibdept/aib.git'     
      mvnHome = tool 'maven'
   }
   stage('Build') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('deploy') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Paib-deploy clean deploy sonar:sonar -Dsonar.host.url=http://ec2-52-207-209-52.compute-1.amazonaws.com:9000/"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}
