pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage ('Build'){
            steps{
                bat 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcatcred', path: '', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'  
                echo "Deployment.."
            }
        }
    }
}
