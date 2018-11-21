pipeline {
    agent any
    stages ('Unit Tests') {
        stage {
            steps {
                sh 'ant -f test.xml -v'
                sh 'reports/result.xml'
            }
        }
    }
    stages ('Build') {
        stage {
            steps {
                sh 'ant -f build.xml -v'
            }
        }
    }
}
