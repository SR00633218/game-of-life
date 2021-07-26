node('GOL') {
    stage('scm') {
       git 'https://github.com/SR00633218/game-of-life.git'
    }
    stage('build'){
        sh 'mvn clean package'
    }
    stage('postbuild'){
        junit '**/TEST-*.xml'
        archive '**/*.war'
    }

}  