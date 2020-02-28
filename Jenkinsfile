
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
		nexusArtifactUploader artifacts: [[artifactId: 'gameoflife', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '95333090-9821-42c8-ae21-8899ee100b04', groupId: 'new', nexusUrl: '3.85.167.144:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'sam123', version: '$BUILD_NUMBER'
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
