pipeline {
	agent any
	stages {
		stage('git url') {
			steps {
				git 'https://github.com/rajachaitanya19/petclinic.git'
			}
		}
		stage('mvn command') {
			steps {
				sh label: '', script: 'mvn clean package'
			}
		}	
		stage('archive artifacts') {
			steps {
				archiveArtifacts 'target/petclinic.war'
			}
		}
		stage('nexus') {
            steps {
				nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: 'target/petclinic.war', type: 'war']], credentialsId: 'nexus', groupId: 'org.springframework.samples', nexusUrl: '13.126.227.171:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: "4.2.${env.BUILD_NUMBER}"
			}
		}
	}
	post { 
        always {
			echo 'I will always say Hello again!'
		}
		success {		
            notify ('success')
		}
		failure {
			notify ('fail')
		}
    }
}
def notify(status) {
	emailext body: "${status}", subject: "${status}", to: 'rajachaitanya19@gmail.com'
}
