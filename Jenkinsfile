pipeline
{
    agent {
        label 'slave'
    }
    tools
    {
        maven 'mvn'
        jdk 'Java'
    }
    options
    {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
    }
    stages
    {
        stage("Cleanup")
        {
            steps
            {
                sh 'mvn clean'
            }
        }
        
        stage("Test")
        {
            steps
            {
                sh 'mvn test'
            }
        }
        stage("Package")
        {
            steps
            {
                sh 'mvn package'
            }
        }
    }
    post
    {
        always
        {
            emailext (attachLog: true, body: '$DEFAULT_CONTENT', subject: '$DEFAULT_SUBJECT', to: 'dipayan.pramanik@knoldus.com')  
        }
        success{
            sh 'echo "--------------------------Deploying------------------------------"'
            sshPublisher(publishers: [sshPublisherDesc(configName: 'Production-Server', transfers: [sshTransfer(cleanRemote: true, excludes: '', execCommand: '''cd Hello-Spring/target
java -jar .jar &''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'Hello-Spring', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/.jar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
            cleanWs()
        }
    }
}

