pipeline {
    agent any
    stages ('Unit Tests') {
        stage {
            steps {
                sh 'ant -f test.xml -v'
                sh 'reports/result.xml'
            }
        }
        stage {
            steps {
                sh 'ant -f build.xml -v'
            }
        }
    }
}
