node(){
    def MavenHome = tool name: 'Maven_3.8.9'
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10')), pipelineTriggers([githubPush()])])
    
    stage('codecheckout'){
    git credentialsId: '66fa58a2-b981-4c49-95d0-9663a2333670', url: 'https://github.com/Tamizh012/maven-web-application.git'
}
    stage('Build'){
         sh "${MavenHome}/bin/mvn clean package"
    }
    stage('Sonar Report'){
         sh "${MavenHome}/bin/mvn sonar:sonar"
    }
    stage('Push to Artifactory'){
         sh "${MavenHome}/bin/mvn deploy"
    }
    stage('Deploy in Tomcat'){
        sshagent(['1d13167a-d977-4c04-9e0f-1c7420f7213a']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@43.204.140.121:/opt/apache-tomcat-9.0.76/webapps/"
}
    }
}  
