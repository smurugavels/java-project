pipeline {
    agent any
    stages {
        stage ('Unit Tests') {
            steps {
                sh 'ant -f test.xml -v'
                junit 'reports/result.xml'
            }
        }
        stage ('Build') {
            steps {
                sh 'ant -f build.xml -v'
            }
        }
        stage ('Deploy') {
            steps {
                sh 'aws s3 cp "${WORKSPACE}/java-pipeline/dist/rectangle-${env.BUILD_NUMBER}.jar" https://s3.console.aws.amazon.com/s3/buckets/assignment10-smurugavels/?region=us-east-1'
            }
        }
    }
}
