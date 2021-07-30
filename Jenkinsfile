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
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to build' )
        choice(name: 'GOAL', choices: ['package', 'clean package', 'install'], description: 'maven goals')
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        retry(2)
    }
    stages {
        stage('scm') {
            steps {
                mail subject: 'BUILD Started '+env.BUILD_ID, to: 'sreenivasrambhatla@gmail.com', from: 'jenkins@qt.com', body: 'EMPTY BODY'
                git branch: "${params.BRANCH}", url: 'https://github.com/SR00633218/game-of-life.git'
            
            }
        }
        stage('build') {
            steps {
                echo env.GIT_URL
                timeout(time:10, unit: 'MINUTES') {
                    sh "mvn ${params.GOAL}"
                }
                stash includes: '**/gameoflife.war', name: 'golwar'
            }
        }
        stage('devserver'){
            agent { label 'RHEL,'}
            steps {
                unstash name: 'golwar'
            }
        }
    }
    post {
        success {
            archive '**/gameoflife.war'
            junit '**/TEST-*.xml'
            mail subject: 'BUILD Completed Successfully '+env.BUILD_ID, to: 'sreenivasrambhatla@gmail.com', from: 'jenkins@qt.com', body: 'EMPTY BODY'
        }
        failure {
            mail subject: 'BUILD Failed '+env.BUILD_ID+'URL is '+env.BUILD_URL, to: 'sreenivasrambhatla@gmail.com', from: 'jenkins@qt.com', body: 'EMPTY BODY'
        }
        always {
            echo "Finished"
        }
        changed {
            echo "Changed"
        }
        unstable {
            mail subject: 'BUILD Unstable '+env.BUILD_ID+'URL is '+env.BUILD_URL, to: 'sreenivasrambhatla@gmail.com', from: 'jenkins@qt.com', body: 'EMPTY BODY'

        }
    }
>>>>>>> 2de31f54c9f585a2a5c8409d2e3f4228fbec9f9d
}