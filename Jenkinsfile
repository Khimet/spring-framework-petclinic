pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-default"
    }

    stages {
        stage('Verify'){
            steps {
                // Verify that Maven is correctly installed
                sh 'mvn -v'
            }
        }
        
        stage('Compile'){
            steps {
                // Maven compilation
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {

                // Run Maven testing
                sh "mvn -Dmaven.test.failure.ignore=true test"
            }
        }
    }
    
    post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    
                    slackSend channel: 'jenkins-training', 
                    message: 'Le build de Khalil a réussi', 
                    teamDomain: 'devinstitut', 
                    tokenCredentialId: '225bcdc5-d7e8-47e6-92ca-9ba05815f67b'
                    //archiveArtifacts 'target/*.jar'
                }
                
                failure {
                    
                    slackSend channel: 'jenkins-training', 
                    message: 'Le build de Khalil a échoué', 
                    teamDomain: 'devinstitut', 
                    tokenCredentialId: '225bcdc5-d7e8-47e6-92ca-9ba05815f67b'
                    
                }
            }
}
