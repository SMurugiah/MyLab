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

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

/*         // Stage 3: Publish Snapshot artifacts to Nexus
        stage ('Publish to Nexus'){
            steps{
                 echo ' publishing......'
         nexusArtifactUploader artifacts: [[artifactId: 'SMLab', classifier: '', file: 'target/SMLab-0.0.1-SNAPSHOT.war', type: 'war']], credentialsId: 'a3494b15-1c5a-4c5b-8636-8ec6b935ec51', groupId: 'com.smdevopslab', nexusUrl: '172.20.10.91:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'SM-Devops-SNAPSHOT', version: '0.0.1'
                echo ' published......'
            }
        } */
		
		// Stage3 : Deploying
        stage ('Deploy'){
            steps {
                echo ' deploying......'

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