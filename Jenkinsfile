pipeline {
    agent{
            label "slave1"
        }
        tools {
            maven 'maven'
            jdk 'jdk 11'
        }
    stages {

        stage('Testing') {
            steps {
                echo 'Testing the application...'
                sh "mvn clean test"
            }
        }
    }
    post {
        success{
        echo "Testing stage successful"
        }
        failure{
        echo "Testing stage failed"
        }
    }
}

