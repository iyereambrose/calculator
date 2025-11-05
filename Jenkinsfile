pipeline {
    agent any

    triggers {
        cron('H/5 * * * *')   // Run the pipeline every 5 minutes
    }

    stages {
        stage("Checkout") {
            steps {
                git url: 'https://github.com/iyereambrose/calculator.git', branch: 'main'
            }
        }

        stage("Compile") {
            steps {
                bat "mvn clean compile"
            }
        }

        stage("Unit Test") {
            steps {
                bat "mvn test"
            }
        }

        stage("Code coverage") {
            steps {
                // Run tests and generate JaCoCo report
                bat "mvn jacoco:report"

                // Publish HTML report
                publishHTML(target: [
                    reportDir: 'target/site/jacoco',
                    reportFiles: 'index.html',
                    reportName: "JaCoCo Report"
                ])

                // Verify coverage thresholds (optional)
                // bat "mvn jacoco:check"
            }
        }
    }
}
