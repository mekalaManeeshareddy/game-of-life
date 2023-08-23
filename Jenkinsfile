pipeline {
    agent { label 'MAVEN_JDK8' }
    triggers { cron ('H/15 * * * *') }
    parameters { 
        string(name: 'MAVEN_GOAL' , defaultvalue: 'package' , description: 'MAVEN_GOAL')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/mekalaManeeshareddy/game-of-life.git,
                    branch: 'declarative'
            }
        }
        stage('package') {
            tools {
                jdk 'jdk_8_ubuntu'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
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
