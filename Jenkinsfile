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
