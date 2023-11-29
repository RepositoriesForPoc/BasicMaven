pipeline {
    agent {label'Window_Agent'}

  // tools {
  //     jdk 'jdk11'}
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/asthagangwar3/BasicMavenProject.git'

                // Run Maven on a Unix agent.
                bat "mvn clean install"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    
                    archiveArtifacts 'target/*.jar'
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('SonarQube') {
            steps {
                withSonarQubeEnv('Sonar') {
                    bat "sonar-scanner"
                }
            }
        }
        
    }
}
