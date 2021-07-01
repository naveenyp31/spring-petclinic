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
            }
        }
        stage('Quality Gate status check'){
            steps{
                withSonarQubeEnv('sonar7.6'){
                   sh 'mvn sonar:sonar'
                }
            }
        }
        stage('upload artifact to repo'){
            steps{
                nexusArtifactUploader artifacts: 
                [[
                    artifactId: 'spring-petclinic', 
                    classifier: '', 
                    file: 'target/petclinic.war', 
                    type: 'war'
                ]], 
                credentialsId: 'nexus-artfact', 
                groupId: 'org.springframework.samples', 
                nexusUrl: '65.0.55.77:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'petclinic-snapshot', 
                version: '4.2.6-SNAPSHOT'
            }
        }
    }
}