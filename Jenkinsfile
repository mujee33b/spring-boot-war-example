pipeline{
    agent any
    tools {
         maven 'Maven' 
    }
    stages{
        stage("Test"){
            steps{
                // mvn test
                sh 'mvn test'
                
            }
        }
        stage("Build"){
            steps{
                //mvn install
                sh 'mvn package'
                
            }
        }
        stage("Deploy on Test Server"){
       post{
        success{
            slackSend channel: 'mail-to-get-notification-in-jenkins', message: 'deploy on test server successfully '
            emailext body: 'delpoy on test ser successfully executed', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
        }
        failure{
            slackSend channel: 'mail-to-get-notification-in-jenkins', message: 'deploy on prod server failed '
            emailext body: 'delpoy on test ser failed', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
        }
    }
            steps{
                // Deploy on container --> plugin
                echo "deploy on test server"
                
                deploy adapters: [tomcat9(credentialsId: '658ab3bd-31a8-4a2f-a2e9-20dcfa0760f7', path: '', url: 'http://65.2.39.54:8080/')], contextPath: '/app', war: '**/*.war'
                
            }
        }
        stage("Deploy on Prod Server"){
            input {
                message "Should we continue?"
                ok "Yes, we should."
            }
             post{
        success{
            slackSend channel: 'mail-to-get-notification-in-jenkins', message: 'deploy on prod server successfully '
            emailext body: 'delpoy on prod ser successfully executed', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
        }
        failure{
             slackSend channel: 'mail-to-get-notification-in-jenkins', message: 'deploy on prod server failed '
            emailext body: 'delpoy on prod ser failed', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
        }
    }
            steps{
                 // Deploy on container --> plugin
                echo "deploy on prod server"
                deploy adapters: [tomcat9(credentialsId: '008dba6a-bc59-4968-8f67-5750191c675f', path: '', url: 'http://13.233.61.83:8080/')], contextPath: '/app', war: '**/*.war'
       
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
             slackSend channel: 'mail-to-get-notification-in-jenkins', message: 'pipeline successfully executed '
            emailext body: 'pipeline successfully executed', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
            echo "========pipeline executed successfully ========"
        }
        failure{
            slackSend channel: 'mail-to-get-notification-in-jenkins', message: 'pipeline failed '
            emailext body: 'pipeline failed', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
            echo "========pipeline execution failed========"
        }
    }
}
