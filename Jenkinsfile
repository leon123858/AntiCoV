pipeline {
	agent none
	stages {
		stage('Run Builds') {
			parallel {
				stage('Build Frontend') {
					when {
						anyOf {
							branch 'master';
							branch 'frontend'
						}
					}
					agent {
						dockerfile {
							filename 'Dockerfile'
							dir 'frontend'
							args '-u root -p 49601:80'
						}
					}
					steps {
						sh './bin/frontend-build.sh'
						input message: 'Finished using the web site? (Click "Proceed" to continue)'
					}
				}
				stage('Build Backend') {
					when {
						anyOf {
							branch 'master';
							branch 'backend'
						}
					}
					agent {
						dockerfile {
							filename 'Dockerfile'
							dir 'backend'
							args '-u root -p 49600:80'
						}
					}
					steps {
						sh './bin/backend-build.sh'
						input message: 'Finished using the web site? (Click "Proceed" to continue)'
					}
				}
			}
		}
	}
}
