pipeline {
    agent any

    //tools {
    //   // Install the Maven version configured as "M3" and add it to the path.
    //    maven "M3"
    //}

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
                //sh "mvn package"
              sh 'true'

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
               always {
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'target/*.jar'
                 emailext body: "${currentBuild.result}", 
                      recipientProviders: [[$class: 'DevelopersRecipientProvider']], 
                      subject: 'Build Notification', 
                      to: 'youremail@example.com'
                }
            }
        }
    }
}


