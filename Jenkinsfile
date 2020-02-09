pipeline {
	agent any
	stages {
		stage('git url') {
			steps {
				git 'https://github.com/swapna-dodda/petclinic.git'
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
		stage('publish arti') {
			steps {
				nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: 'releases', type: 'war']], credentialsId: 'nexus', groupId: 'org.springframework.samples', nexusUrl: '13.126.43.39:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'target/petclinic.war', version: '4.2.6'
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
	emailext body: "${status}", subject: "${status}", to: 'dswapna1906@gmail.com'
}
