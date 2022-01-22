pipeline{
    agent{
        label "aws_node"
    }
    tools{
        maven 'mavenhome' 
    }
    stages{
        stage("Test"){
            steps{
                sh "mvn --version"
                sh 'mvn test'
            }  
        }
        stage("SonarQube"){
            steps{
             
                sh 'mvn sonar:sonar'
            }  
        }
        stage("Build"){
            steps{
                sh 'mvn package'
            }  
        }
        stage("Deploy"){
            steps{
                deploy adapters: [tomcat9(credentialsId: '48cad2b3-6227-489d-83a4-e3508346fbc3', path: '', url: 'http://18.221.95.100:8080')], contextPath: 'sample', war: '**/*.war'
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
