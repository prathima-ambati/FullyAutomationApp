pipeline{

agent any

stages{
stage('Build'){
steps{
bat label: '', script: 'mvn clean package'
}
post{
success{
echo 'archiving war file'
archiveArtifacts '**/*.war'
}
failure{
echo 'faied to archive'
}
}
}
stage('Deploy to staging'){

steps{
   deploy adapters: [tomcat9(credentialsId: 'ae93a917-b683-44de-a21b-17f00ccac8e9', path: '', url: 'http://localhost:8223')], contextPath: null, war: '**/*.war'
}
post{
success{
echo 'deployment successfull into staging'

}
failure{
echo 'faied to deploy into staging'
}

}
}
stage('Deploy to production'){

steps{


  deploy adapters: [tomcat9(credentialsId: 'b7b0e00a-a7bd-46f7-b1f8-e77d00c86b89', path: '', url: 'http://localhost:8224')], contextPath: null, war: '**/*.war'
}
post{
success{
echo 'deployment successfull'

}
failure{
echo 'faied to deploy'
}

}
}

}
}