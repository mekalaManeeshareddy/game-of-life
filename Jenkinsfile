pipeline {
    agent { label 'MAVEN_JDK8' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/khajadevopsmarch23/game-of-life.git',
                    branch: 'declarative'
            }
        }
        stage('package') {
            tools {
                jdk 'jdk_8_ubuntu'
            }
            steps {
                sh 'mvn package'
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}
