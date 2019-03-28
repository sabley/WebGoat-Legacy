node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */
        sh 'mvn clean package'
    }
/*
    stage('Test image') {
        
        nexusPolicyEvaluation failBuildOnNetworkError: false, iqApplication: manualApplication('webgoat'), iqStage: 'build', jobCredentialsId: ''
    }*/
    stage('Publish to NXRM') {
        
        nexusPublisher nexusInstanceId: 'nxrm3', nexusRepositoryId: 'maven-snapshots', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/WebGoat-6.0.1.war']], mavenCoordinate: [artifactId: 'webgoat', groupId: 'com.yourcompany', packaging: 'war', version: '6.0.1']]]
    }	
/*
    stage('Push image') {
         
			You would need to first register with DockerHub before you can push images to your account
		
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }*/
}
