pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage 2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage 3 : Publish over ssh
        stage ('Publish'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'EmmaDevOpsLab', classifier: '', file: 'target/EmmaDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'Nexus', groupId: 'com.emmadevopslab', nexusUrl: '172.20.10.186:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'EmmaDevopsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'

            }
        }


       // Stage 4 : Deployment
         stage ('Deploy'){
            steps {
                echo ' deploying......'
            }   

        
        
        } 
    
    
    }


}

