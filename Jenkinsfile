pipeline{
    agent{
        label "master"
    }
    tools { 
        maven 'maven' 
        jdk 'jdk 11'
    }
    stages{
        stage("building"){
            steps{
                sh "mvn clean package"
            }
        }

    }
    post{
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}

