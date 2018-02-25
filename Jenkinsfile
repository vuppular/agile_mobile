    node {
	    deleteDir()
        def server = Artifactory.server 'central'
        def rtMaven = Artifactory.newMavenBuild()
        def buildInfo
        
        //def javaHome = tool name: 'java1.8', type: 'hudson.model.JDK'
        //def mvnHome = tool name: 'maven3', type: 'hudson.tasks.Maven$MavenInstallation'
	rtMaven.tool = 'maven3'
        
        timestamps {
             
                stage("Initialize Build") {
                    echo "EXECUTING ON THE NODE: $env.NODE_NAME"
			echo "*************BRANCH1***********************"
          
                }
                 // Mark the code checkout 'stage'.... . . 
                stage ('Checkout') {
                   // Checkout code from repository
                   checkout scm
                 }

                stage('Artifactory configuration') {
                    rtMaven.tool = 'maven3'
                    rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
                   // rtMaven.resolver releaseRepo: 'repo', snapshotRepo: 'repo', server: server
                    buildInfo = Artifactory.newBuildInfo()
                    rtMaven.deployer.deployArtifacts = false // Disable artifacts deployment to artifactory
                }
                stage('mvn goals execution') {
                    rtMaven.run pom: 'pom.xml', goals: 'clean release:clean release:prepare release:perform'
		    
		 }
            
        }
    }
