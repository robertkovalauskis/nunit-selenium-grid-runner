pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				bat "docker pull kovalauskis/nunit-selenium-grid"
			}
		}
		stage("Start Grid"){
			steps{
				bat "docker-compose up -d hub chrome firefox"
			}
		}
		stage("Run Test"){
			steps{
				bat "docker run -e CATEGORY=Smoke -v ./output/test-results:/usr/share/test-output kovalauskis/nunit-selenium-grid"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			bat "docker-compose down"
			bat "sudo rm -rf output/"
		}
	}
}