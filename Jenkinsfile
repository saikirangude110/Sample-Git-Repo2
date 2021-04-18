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

        stage ("Deploying Artifact to tomcat server") {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible_sever', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo ansible-playbook /etc/ansible/playbooks/deploy-artifact.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'Tasks/Tasks-1/Jenkins_Pipeline/target/', sourceFiles: 'Tasks/Tasks-1/Jenkins_Pipeline/target/trucks.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
	    }
	}
    }      
}
