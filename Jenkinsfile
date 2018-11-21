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
                echo 'usr/bin/aws s3 cp "${WORKSPACE}/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar" s3://assignment10-smurugavels/rectangle-${BUILD_NUMBER}.jar'                
            }
        }
        stage ('Output') {
            step {
                withCredentials([$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']) {
                    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
                }
            }
        }
    }
}
