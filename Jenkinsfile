pipeline{
	
	agent any
	
	environment{
		LANG='en_US.UTF-8'
		LC_ALL='en_US.UTF-8'
	}
	
	tools{
		maven 'Maven'
		jdk 'JDK'
	}
	
	stages{
		stage('Checkout'){
			steps{
				git master:'master',url:'https://github.com/ShashiMadari/practice2.git'
			}
		}
		
		stage('Build'){
			steps{
				sh 'mvn clean package'
			}
		}
		
		stage('Archive'){
			steps{
				archiveArtifacts artifacts:'target/*',fingerprint:true
			}
		}
		
		stage('Deploy'){
			steps{
				sh 'mvn clean package'
				sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
			}
		}
	}
	
	post{
		success{
			echo 'Success'
		}
		failure{
			echo 'fail'
		}
	}
}
