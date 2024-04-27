pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3"
        jdk "jdk-17"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                //git url: 'https://github.com/K4szmiriX/jenkins-course-repo.git', branch: 'master'
                git url: 'https://github.com/rechandler12/szkolenie-ci-jenkins-example.git', branch: 'main'

                // Run Maven on a Unix agent.
                sh "mvn clean install"
            }
        }
    }

    post {
        // If Maven was able to run the tests, even if some of the test
        // failed, record the test results and archive the jar file.
        success {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
            slackSend color: "good", message: "Message from Jenkins Pipeline"
        }
    }
}
