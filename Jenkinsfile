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

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

/*         // Stage 3: Publish Snapshot & Release artifacts to Nexus -- Working
                
        stage ('Publish to Nexus'){
            steps{
                 echo ' publishing......'
         nexusArtifactUploader artifacts: 
         [[artifactId: 'SMLab', 
         classifier: '', 
         file: 'target/SMLab-0.0.1-SNAPSHOT.war', 
         type: 'war']], 
         credentialsId: 'a3494b15-1c5a-4c5b-8636-8ec6b935ec51', 
         groupId: 'com.smdevopslab', 
         nexusUrl: '172.20.10.91:8081', 
         nexusVersion: 'nexus3', 
         protocol: 'http', 
         repository: 'SM-Devops-SNAPSHOT', 
         version: '0.0.1-SNAPSHOT'
                echo ' published......'
            }
        } */
		
        //  Stage 3: Publish Snapshot & Release artifacts to Nexus -- Using Scripts
        stage ('Publish to Nexus using Scripts'){
             steps {
                script {

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "SM-Devops-SNAPSHOT" : "SM-Devops-RELEASE"

                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}",
                 classifier: '', 
                 file: "target/${ArtifactId}-${Version}.war", 
                 type: 'war']], 
                 credentialsId: 'a3494b15-1c5a-4c5b-8636-8ec6b935ec51', 
                 groupId: "${GroupId}", 
                 nexusUrl: '172.20.10.91:8081', 
                 nexusVersion: 'nexus3', 
                 protocol: 'http', 
                 repository: "${NexusRepo}", 
                 version: "${Version}"
             }
            }
        }

             //  Stage 4: Print Variables
        stage ('Print Environment Variables'){
            steps{
                 echo " Artifact ID is '${ArtifactId}'"
                 echo " Version is '${Version}'"
                 echo " Group ID is '${GroupId}'"
                 echo " Name is '${Name}'"

            }  
        }



		// Stage5 : Deploying
        stage ('Deploy'){
            steps {
                echo ' deploying......'

                /* sshPublisher(publishers:
                [sshPublisherDesc(
                    configName: 'Ansible_Controller',
                    transfers: [
                        sshTransfer(
                        cleanRemote: false, 
                        execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy.yaml -i /opt/playbooks/hosts', 
                        execTimeout: 120000)
                        ], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)

                    ]
                ) */

        sshPublisher(publishers: 
        [sshPublisherDesc(
            configName: 'Ansible Controller', 
        transfers: [sshTransfer(
            cleanRemote: false, 
            excludes: '', 
            execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy.yaml -i /opt/playbooks/hosts', 
            execTimeout: 120000, 
            flatten: false, 
            makeEmptyDirs: false, 
            noDefaultExcludes: false, 
            patternSeparator: '[, ]+', 
            remoteDirectory: '', 
            remoteDirectorySDF: false, 
            removePrefix: '', 
            sourceFiles: '')], 
            usePromotionTimestamp: false, 
            useWorkspaceInPromotion: false, 
            verbose: false
            )
        ]
    )
            }
        }

        // Stage3 : Publish the source code to Sonarqube
   //     stage ('Sonarqube Analysis'){
    //        steps {
    //            echo ' Source code published to Sonarqube for SCA......'
    //            withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
    //                 sh 'mvn sonar:sonar'
     //           }

     //       }
      //  }

        
        
    }

}