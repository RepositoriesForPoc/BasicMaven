pipeline {
    agent {label'Window_Agent'}

  
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/RepositoriesForPoc/BasicMaven.git'

                // Run Maven on a windows agent.
                bat "mvn clean install"

               
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
