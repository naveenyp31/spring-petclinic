pipeline{
    agent{
        label "dev"
    }
    tools{
        maven 'maven381'
    }
    stages{
        stage('checkout'){
            steps{
                git credentialsId: 'Git_cred', 
                url: 'https://github.com/naveenyp31/spring-petclinic.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package -DskipTests'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
                junit allowEmptyResults: true, testResults: 'target/surefire-reports/*xml'
            }
        }
    }
}