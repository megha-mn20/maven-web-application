node('master')
{ def MavenHome= tool name: "Maven-3.6.3"
    stage('CheckOutCode')
    {git branch: 'development', credentialsId: '238c7280-91eb-4f35-a5a4-b65731f40909', url: 'https://github.com/megha-mn20/maven-web-application.git'
    }
    
    stage('BuildTheCode')
    {
        sh "${MavenHome}/bin/mvn clean package"
    }
    
    stage('Sonarreport')
    {
        sh "${MavenHome}/bin/mvn sonar:sonar"
    }
    stage('TouploadartifactIntoNexus')
    {
        sh "${MavenHome}/bin/mvn deploy"
    }
      stage('ToDeployapplicationToTomcat')
     { 	sshagent(['8807f5b1-84f2-4dd2-a061-d2f7270fa72b']) {
			sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.2.5.232:/opt/apache-tomcat-9.0.44/webapps/" }
    
     }
     stage('email')
     { 
     emailext body: '''Hello
scriptedway''', subject: 'pipeline-scriptedway', to: 'meghabvk1@gmail.com'
}

}

  
