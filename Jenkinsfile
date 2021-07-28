pipeline {
    agent {label 'GOL'}
    stages{
        stage('SCM'){
            step{
                git branch: 'master', url:https://github.com/SR00633218/game-of-life.git
            }
        }
        stage('build') {
            steps {
                sh 'mvn package'
    }
    post {
        sucess{
            archive '**/gameoflife.war'
            junit '**/TEST-*.xml'

        }
        
    }

}