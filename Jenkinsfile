pipeline {
    agent any

    triggers {
        cron('H/5 * * * *') // Run every 5 minutes
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
                bat "mvn jacoco:report"

                publishHTML(target: [
                    reportDir: 'target/site/jacoco',
                    reportFiles: 'index.html',
                    reportName: "JaCoCo Report"
                ])
            }
        }
    }

    post {
        always {
            mail(
                to: 'iyereambrose60@gmail.com',
                subject: "Completed Pipeline: ${currentBuild.fullDisplayName}",
                body: """Your build is complete.
Build status: ${currentBuild.currentResult}
Check details at: ${env.BUILD_URL}"""
            )
        }
    }
}
