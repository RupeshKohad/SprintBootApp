pipeline{
    agent{
        label "Linux_Node"
    }
    tools{
        maven 'maven_home' 
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
                deploy adapters: [tomcat9(credentialsId: '36e36ab9-5dcc-4abf-ad22-8cb2a425965c', path: '', url: 'http://54.152.32.154:8080')], contextPath: 'sample', war: '**/*.war'
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
