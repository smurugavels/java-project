pipeline {
    agent any
    environment {
        AWS_ID = credentials("AWS_ID")
        AWS_ACCESS_KEY_ID = "${env.AWS_ID_USR}"
        AWS_SECRET_ACCESS_KEY = "${env.AWS_ID_PSW}"
    }
    stages {
        stage ('Unit Tests') {
            steps {
                sh 'echo $AWS_ID'
                sh 'echo AWS_ACCESS_KEY_ID'
                sh 'echo AWS_SECRET_ACCESS_KEY'
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
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
                                  accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                                  credentialsId: '762130a261ec-762130a261ec-762130a261ec',
                                  secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
                }
            }
        }
    }
}
