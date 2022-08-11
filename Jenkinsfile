pipeline {
    agent any
    triggers {
        cron('H * * * *')
    }

    stages {
        
        stage('Checkout'){
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/esti31r/jgsu-spring-petclinic.git', branch: 'main'
            }
        }
        stage('Validation') {
            steps {
            sh "./mvnw validate"
            }
        }
        
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "./mvnw clean package"
            }
        }
        
        stage('Test') {
            steps {
            sh "./mvnw test"
            }
        
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
            
        }
    }
}
