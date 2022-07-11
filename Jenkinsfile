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


        // Stage 3 : Publishing
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.18:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'EmmaDevopsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'

            }
        }

        // Stage 4 : Deploying
        stage ('Deploy'){
            steps {
                echo 'deploying......'

            }
        }



       

        
        
    }

}