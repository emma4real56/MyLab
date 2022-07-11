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

        //Stage 3: Publish the Artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'EmmaDevOpsLab', classifier: '', file: 'target/EmmaDevopsLab-0.0.4-SNAPSHOT', type: 'war']], credentialsId: '12e0c126-fec2-4659-9f64-cd70d55b0dde', groupId: 'com.emmadevopslab', nexusUrl: '172.20.10.18:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'EmmaDevopsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
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