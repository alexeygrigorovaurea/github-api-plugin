pipeline {
    agent {
        label 'linux'
    }
    stages {
        stage('Build github api plugin') {
            steps {
                dir('github') {
                    git branch: 'master', credentialsId: 'engbuild-github-credentials',
                        url: 'https://github.com/trilogy-group/eng-build-jenkins-github-api'
                }
                sh 'cd github; mvn clean install -DskipTests -DskipITs; cd ..'
                sh 'mvn clean package  -DskipTests -Dmaven.javadoc.skip=true; cp target/github-api-plugin.hpi target/github-api-plugin.jpi.override'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'target/github-api-plugin.jpi.override', fingerprint: true
        }
    }
}
