def mymethod(String name = 'human') {
  echo "Hello, ${name}."
  echo "Hello, ${name}."
}


node('maven-label') {
   def mvnHome
   
   stage(){
    mymethod "Intellipath"  
   }
   stage('Preparation') { 
      
      git 'https://github.com/cardrandd/bcard-app.git'
          
      mvnHome = tool 'maven'
   }
   stage('Build') {
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
