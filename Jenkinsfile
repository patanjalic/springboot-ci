pipeline {
   agent any
   tools {
        maven 'M3'
        jdk 'jdk1.8'
    }
   stages {
      stage('Build') {
         steps {
            // Run the maven build
            sh 'mvn -f pom.xml -Dmaven.test.failure.ignore clean package'
         }
      }
      stage('Deploy') {
         steps {
            script {
               if (currentBuild.result == null || currentBuild.result == 'SUCCESS') {
                  //timeout(time: 30, unit: 'SECONDS') {
                      // you can use the commented line if u have specific user group who CAN ONLY approve
                      //input message:'Approve deployment?', submitter: 'it-ops'
                      //input message: 'Approve deployment?'
                  //}
                  echo "proceeded to next step"
                  sh 'cp target/*.jar /c/springboot/deployments'
                  sh 'java -jar /c/springboot/deployments/*.jar'
               }  
            }
         }
      }
      stage('Results') {
         steps {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
         }
      }
   }
}
