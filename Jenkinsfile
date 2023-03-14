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
                deploy adapters: [tomcat9(credentialsId: '17fcd11e-8b88-4835-b2bd-a3b42faf1414', path: '', url: 'http://65.2.39.54:8080/')], contextPath: '/app', war: '**/*.war'
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
