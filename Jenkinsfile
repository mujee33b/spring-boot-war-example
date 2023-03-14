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
            steps{
                // Deploy on container --> plugin
                echo "deploy on test server"
               deploy adapters: [tomcat9(credentialsId: '658ab3bd-31a8-4a2f-a2e9-20dcfa0760f7', path: '', url: 'http://65.2.39.54:8080/')], contextPath: '/app', war: '**/*.war'
                emailext body: 'delpoy on test ser passed successfully', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
            }
        }
        stage("Deploy on Prod Server"){
            input {
                message "Should we continue?"
                ok "Yes, we should."
            }
            steps{
                 // Deploy on container --> plugin
                echo "deploy on prod server"
                emailext body: 'passed successfully', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
                deploy adapters: [tomcat9(credentialsId: '008dba6a-bc59-4968-8f67-5750191c675f', path: '', url: 'http://13.233.61.83:8080/')], contextPath: '/app', war: '**/*.war'
                emailext body: 'deploy on prod ser passed successfully', subject: 'test for success notification', to: 'mohdabdulmujeeb55@gmail.com'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
