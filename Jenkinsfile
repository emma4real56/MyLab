pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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


        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
              

                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'Nexus', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.18:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "EmmaDevopsLab-SNAPSHOT", 
                version: "${Version}"
             }
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

