pipeline {
    options {
        buildDiscarder(logRotator(numToKeepStr: "10"))
    }
    agent any

    stages {
        stage('Stage sh') {
            steps {
                echo 'Waiting a bit'
                sh "sleep 1"
                echo 'Done with stage'
            }
        }
    }
}
