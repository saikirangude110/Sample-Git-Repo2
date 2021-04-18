pipeline {
        agent {label 'Jenkins_Node_1'}

    stages {

        stage ("Getting Souce Code From Git") {
            steps {
                git 'https://github.com/saikirangude/Git-repo2.git'
            }
        }
        stage ("SonarQube analysis") {
            steps {
                withSonarQubeEnv('SonarQube_Scanner') {
                    sh 'mvn clean sonar:sonar'
                }
            }
		  }
			
        stage ("cleaning build classes") {
            steps {
                sh 'mvn clean'
            }
        }

        stage ("Compiling The Source Code") {
            steps {
                sh 'mvn compile'
            }
        }

        stage ("Testing The Source Code") {
            steps {
                sh 'mvn test'
            }
        }

        stage ("Generating Artifact") {
            steps {
                sh 'mvn package'
            }
        }
    }      
}
