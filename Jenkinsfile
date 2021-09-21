#!/usr/bin/env groovy

pipeline {
    environment {
		registry = "docker pull nagnutakki9/testing"
		registryCredential = 'Cloudscape_2017'
	}
	agent { label 'master' }

	stages {
        stage ('Checkout') {
			steps{
        	git clone "https://github.com/nagnutakki9/multipipeline.git"
        }
	}
		stage ('Docker Push') {
		    steps{
              script {
                sh "docker log -u nagnutakki9 -p Cloudscape_2017"
              }
            }
			steps{
			    sh "pwd"
				sh "ansible-playbook ansible/docker_build.yml"
			}	
        }
		stage ('Test latest build') {
		    steps{
              script {
                sh "echo 'Testing newly build image'"
              }
            }
        }
		stage ('Docker tag as latest') {
		    steps{
              script {
                sh "echo 'If it is a stable build the tag as latest and push'"
				sh "ansible-playbook ansible/docker_latest_tag.yml"
              }
            }
        }

      	stage ('Kubernetes Deploy') {
			  steps{
            	sh "ansible-playbook ansible/main.yml"
			  }
      	} 
	}
}
