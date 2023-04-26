pipeline {
    agent any

    //tools {
    //   // Install the Maven version configured as "M3" and add it to the path.
    //    maven "M3"
    //}
    triggers { pollSCM('* * * * *')}
    stages {
        stage('Chckout fromm git') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/inveon-cudiunal/jgsu-spring-petclinic.git'
            }
            
        }
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
               success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                    def subject = "Email Subject"
                    def body = "Email Body"
                    def recipient = "example@example.com"

                    mailer = Jenkins.instance.createProject(Mailer.class, "mailer")
                    mailer.sendMail(
                    recipient,
                    new TextBody(body),
                    new TextBody(subject)
)
                }
            }
        }
    }
}


