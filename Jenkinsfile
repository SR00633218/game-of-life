pipeline {
    agent {label 'GOL'}
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to build' )
        choice(name: 'GOAL', choices: ['package', 'clean package', 'install'], description: 'maven goals')
        choice(name:'JDK', choices:['JDK8', 'JDK11'], description: 'JDK version')
    }
    stages {
        stage ('SCM') {
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/SR00633218/game-of-life.git'
            }
        }
        stage ('build') {
            steps {
                 sh 'mvn package'
            }
        }
        post {
            success {
                archive '**/gameoflife.war'
                junit '**/TEST-*.xml'
            }
            
            
        }
    }
}