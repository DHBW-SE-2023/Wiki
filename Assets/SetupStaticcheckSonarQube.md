# Staticcheck

By running '''staticcheck ./...''' locally, staticcheck checks the code locally for code smells.

# Sonar

## Setup

'''docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest'''
Follow the guide to create a local YAAC project and run the generated sonar-scanner command in YAAC's root folder. You may also want to use the SonarLint VSCode Extension (requires an installation of the JRE).