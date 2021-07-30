pipeline {
<<<<<<< HEAD
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
=======
    agent { label 'GOL'}
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to build' )
        choice(name: 'GOAL', choices: ['package', 'clean package', 'install'], description: 'maven goals')
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        retry(2)
    }
    environment {
        CI_ENV = 'DEV'
    }
    stages {
        stage('scm') {
            environment {
                DUMMY = 'FUN'
            }
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/SR00633218/game-of-life.git'
                echo env.CI_ENV
                echo env.DUMMY
            }
        }
        stage('build') {
            steps {
                echo env.GIT_URL
                timeout(time:10, unit: 'MINUTES') {
                    sh "mvn ${params.GOAL}"
                }
                
            }
        }
    }
    post {
        success {
            archive '**/gameoflife.war'
            junit '**/TEST-*.xml'
        }
       
        
    }
>>>>>>> 2de31f54c9f585a2a5c8409d2e3f4228fbec9f9d
}