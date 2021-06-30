pipeline{
    agent{
        label "dev"
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
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
}