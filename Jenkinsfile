pipeline {
    agent any
    stages {
        stage ('Unit Tests') {
            steps {
                sh 'ant -f test.xml -v'
                sh 'reports/result.xml'
            }
        }
        stage ('Build') {
            steps {
                sh 'ant -f build.xml -v'
            }
        }
    }
}
