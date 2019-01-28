node('maven-label') {
   def mvnHome
   stage('Preparation') { 
      
      git 'https://github.com/aibdept/aib.git'     
      mvnHome = tool 'maven'
   }
   
   stage('deploy') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Paib-deploy clean deploy sonar:sonar"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }bbb
}
