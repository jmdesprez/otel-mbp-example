pipeline {
    agent any
    stages {
        stage('Stage-0 new naming') {
            steps {
                withMockLoad(averageDuration: 3, testFailureIgnore: false) {
                    sh MOCK_LOAD_COMMAND
                }
            }
        }
        stage('Stage-1') {
            parallel {
                stage('Stage-1.1') {
                    agent {label "agent-1"}
                    steps {
                        sh "echo 'first step ON DEMO!!!!'"
                        withMockLoad(averageDuration: 3, testFailureIgnore: false) {
                            sh MOCK_LOAD_COMMAND
                        }
                        sh "echo 'Execution completed'"
                    }
                }
                stage('Stage-1.2') {
                    stages {
                        stage('1.2.1') {
                            steps {
                                withMockLoad(averageDuration: 9, testFailureIgnore: false) {
                                    sh MOCK_LOAD_COMMAND
                                }
                            }
                        }
                        stage('1.2.2') {
                            agent {label "agent-1"}
                            steps {
                                withMockLoad(averageDuration: 9, testFailureIgnore: false) {
                                    sh MOCK_LOAD_COMMAND
                                }
                            }
                        }   
                    }
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn clean test'
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
}
