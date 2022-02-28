properties([pipelineTriggers([githubPush()])])

pipeline {
     agent any
     stages {
          stage("Change Request") {
               when { changeRequest() }
               steps {
                    sh "uname -a; date"
               }
          }
	  stage("Compile") {
               steps {
                    sh "./gradlew compileJava"
               }
          }
          stage("Unit test") {
               steps {
                    sh "./gradlew test"
               }
          }
          stage("Code coverage") {
               when { branch "main" }
	       steps {
                    sh "./gradlew jacocoTestReport"
                    sh "./gradlew jacocoTestCoverageVerification"
               }
          }
          stage("Static code analysis") {
               steps {
                    sh "./gradlew checkstyleMain"
               }
          }
	  stage("Checkstyle added") {
	      steps {
		   sh "./gradlew checkstyleTest"
	      }
          }
          stage("Package") {
               steps {
                    sh "./gradlew build"
               }
          }
     }
}
