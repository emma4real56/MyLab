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
                script {

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "EmmaDevopsLab-SNAPSHOT" : "EmmaDevopsLab-RELEASE"

                nexusArtifactUploader artifacts:  
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'Nexus', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.186:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
             }
            }  
        }


        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
        
        }


        // Stage 5 : Deploy
        stage ('Deployment'){
            steps {
                echo "Deploying......"
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'Ansible-Control', 
                    transfers: [
                        sshTransfer(
                            cleanRemote: false, 
                            execCommand: 'ansible-playbook /home/ec2-user/control/exercise1/download.yaml -i /home/ec2-user/control/exercise1/inventory', 
                            execTimeout: 120000
                        )     
                    ], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)
                    ])
                

            }
        }
    
    
    }  

}

