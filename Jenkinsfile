pipeline {
     agent any
     triggers {
     pollSCM('H/5 * * * *')
     }
     stages {
          stage("Checkout") {
               steps {
                    git url: 'https://github.com/iyereambrose/calculator.git', branch: 'main'
               }
          }
          stage("Compile"){
              steps {
                  bat "mvn clean compile"
              }
          }
          stage("Unit Test"){
              steps {
                  bat "mvn test"
              }
          }
          stage("Code coverage") {
              steps {
                  // Run tests and generate JaCoCo report
                  bat "mvn jacoco:report"

                  // Publish HTML report
                  publishHTML (target: [
                      reportDir: 'target/site/jacoco',
                      reportFiles: 'index.html',
                      reportName: "JaCoCo Report"
                  ])

                  // Verify coverage thresholds
                  //bat "mvn jacoco:check"
              }
          }

     }
}