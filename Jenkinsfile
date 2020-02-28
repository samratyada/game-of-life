
 pipeline 
{
agent any
tools
{
maven "maven"
}
stages {
stage('Gitcheckout')
{
steps{
git 'https://github.com/samratyada/game-of-life.git'
}
}
stage('Maven conf')
{
steps {
sh label: '', script: 'mvn clean package'
}
}
      
//stage('sonarqube') {
  //environment 
  //{
   //def scannerHome = tool 'sonarqube'
    //}
   //steps {
     //   withSonarQubeEnv('sonarqube') {
       //sh "${scannerHome}/bin/sonar-scanner"
//}
  //  timeout(time: 10, unit: 'MINUTES') {
    // waitForQualityGate abortPipeline: true
     //}
	//  }
      //}
	
	stage ('Nexus storage')
	{
		steps {
nexusPublisher nexusInstanceId: '1234', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'var/lib/jenkins/gemeoflife.war']], mavenCoordinate: [artifactId: 'ravi', groupId: '1234', packaging: 'war', version: '$BUILD_ID']]]
}
}
stage ('Deploy war')
{
steps {
sh label: '', script: 'ansible-playbook deploy.yml'
    }
  }
 }
}  
