pipeline{
    agent {
        node {
            label 'maven'
        }
    }

environment {
    PATH = "/opt/apache-maven-3.9.7/bin:$PATH"
}
    stages {
        stage('build') {
            steps {
                sh 'mvn clean deploy'
            }
        }
        stage('test') {
            steps {
                echo "----unit test started-----"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "----unit test completed-----"
            }
        }
        stage('SonarQube analysis') {
        environment {
            scannerHome = tool 'sonar-scanner'
        }
        steps {
        withSonarQubeEnv('sonarqube-server') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        }
        }
    }
}
