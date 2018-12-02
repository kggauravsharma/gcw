node("maven-label") {
   def mvnHome
   def branch='dev'
   stage('Preparation') { 
      git branch: '${branch}', credentialsId: 'vagrant-git', url: 'git@github.com:devops24th/gcw.git'
             
      mvnHome = tool 'maven'
   }
   stage('Build') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
