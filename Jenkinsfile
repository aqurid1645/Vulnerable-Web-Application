pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch:'main', url: 'https://github.com/aqurid1645/ICT2216-SSD-Group-16.git'
            }
        }

        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                    sh "/var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://192.168.1.25:9000/ -Dsonar.token=sqp_c5e6dad39519d0f5a964cca6ff47d57606db72a6"
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