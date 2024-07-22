pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
            }
        }

        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                    sh "/var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://192.168.1.25:9000/ -Dsonar.token=sqp_c3bfe5f6c78cca370718e53e21a5463cea58578b"
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}