pipeline {
	agent any
	environment {
		RELEASE='20.04'
	}
	stages {
		stage("Build") {
			environment {
				LOG_LEVEL="INFO"
			}
			steps {
				echo "Building releases ${RELEASE} with log level ${LOG_LEVEL}"
			}
			parallel {
				stage("Linux-arm64") {
					steps {
						echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}"
					}
				}
				stage("Linux-amd64") {
					steps {
						echo "Building release ${RELEASE} for ${STAGE_NAME} with log level ${LOG_LEVEL}"
					}
				}
			}
		}
		stage("Test") {
			steps {
				echo "Testing. I can see release ${RELEASE}"
				}
		}
		stage("Deploy") {
			input {
				message 'Deploy'
				ok 'Do it'
				parameters {
					string(name: "TARGET_ENVIRONMENT", defaultValue: "PROD", description: "Target deployment environment")
				}
			}
			steps {
				echo "Deploying release ${RELEASE} to environment ${TARGET_ENVIRONMENT}"
			}
		}
	}
	post {
		always {
			echo "Print whatever deploy happened or not, success of failure"
		}
	}


}
