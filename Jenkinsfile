@Library('pipeline-library-demo')_


def mymethod(String name = 'human') {
  echo "Hello, ${name}."
  echo "Hello, ${name}."
}


node('maven-label') {
   def mvnHome
   
   stage('ref-lib'){
    mymethod 'Intellipath'
    sh "cd $WORKSPACE && python a.py" 
   }
  
  stage('Demo') {
    echo 'Hello World'
    sayHello 'Dave'
   }
   stage('Preparation') { 
      
      git 'https://github.com/cardrandd/bcard-app.git'
          
      mvnHome = tool 'maven'
   }
   stage('Build') {
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package sonar:sonar -Dsonar.host.url=http://ip-172-31-44-182.ap-south-1.compute.internal:9000/'
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
