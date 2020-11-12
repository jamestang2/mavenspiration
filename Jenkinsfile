pipeline {
   agent any

   tools {
      maven "MVN"
   }

   stages {
        stage('Build') {
            steps {
                git 'https://github.com/javaee/cargotracker.git'
            
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage ('Upload Nexus') {
            steps {
                nexusPublisher nexusInstanceId: 'demo0.1', nexusRepositoryId: 'demo0.1', 
                packages: [[$class: 'MavenPackage', 
                mavenAssetList: [[classifier: '', extension: '', filePath: '\\target\\cargo-tracker.war']], 
                mavenCoordinate: [artifactId: 'nexus-upload', groupId: 'test.maven', packaging: 'war', version: '0.1']]]
            }
        }
    }
}
