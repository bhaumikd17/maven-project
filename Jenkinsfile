pipeline{
agent any
tools {
jdk 'Java_8'
maven 'mvnproject'
}
stages {

 stage("First Stage") {

     steps {

       echo "This is First Stage:"        
     }
 }
  stage('Staging:') {

     steps {

       echo "This is Staging Stage:" 
       sh 'mvn clean package checkstyle:checkstyle'

     }
    post {
    success {

        echo "Checkstyle report"
        checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'checkstyle:checkstyle', unHealthy: ''
        echo "Archive Artifacts"
        archiveArtifacts '**/*.war'
        echo "JUnit Report"
        //junit '**/target*surefire-report/*.xml'
        junit '*/target/surefire-reports/*.xml'

    }
  }
 }

 stage('Deployment Stage:') {

     steps {

       echo "This is Deployment Stage:" 
       build 'Staging'
       echo "Successfully Deployed:"
       
     }
 }

 stage('Production Stage:') {

     steps {

       timeout(1) 
       {
          input 'Would you like to deploy? '

       }
       echo "This is Production Stage:" 
       build 'Production Server'

       //echo "Successfully Deployed:"
       
     }
 }

}
}
