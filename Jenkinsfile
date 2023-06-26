pipeline {
	agent {label "agentfarm" }
	stages {
		stage('Installing Maven') {
			steps {
				sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
				sh 'sudo apt-get install -y wget tree unzip maven'
			}
		}
		stage('Compiling and Running Test Cases') {
			steps {
				sh 'mvn clean'
				sh 'mvn compile'
				sh 'mvn test'
				}
			}
		stage('Creating Package') {
			steps {
				sh 'mvn package'
				}
			}
               stage ('Deploying Application Using Ansible') {

			steps {
				sh 'export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook --private-key=/home/ubuntu/.ssh/vm-instance-key.pem -i host_inventory deploy-artifact.yml'
				}

			}	
           }
	}	
