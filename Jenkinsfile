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
                sh "which aws"
                sh (" /usr/bin/aws s3 cp ${WORKSPACE}/dist/rectangle-${BUILD_NUMBER}.jar s3://assignment10-smurugavels/rectangle-${BUILD_NUMBER}.jar")              
            }
        }
        stage ('Output') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '26d64cd7-11fe-412b-942a-2210b467c7d3', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    sh (" /usr/bin/aws aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins")
                }
            }
        }
    }
}
