pipeline
{
  agent any

  tools
  {
  maven "maven-3.9.8"
  }

  stages
  {

     stage('checkout')
     {

       steps
       {
        git branch:'master', credentialsId: '50c39f0f-d1ca-4f94-b30e-d318c3488c8a', url: 'https://github.com/my-projects-shiv/maven-web-app-project-shivdev.git'
        }
     }
     stage ('COMPILE') {
         steps {
             sh "mvn clean compile"
         }
     }
     
     stage ('BUILD') {
         steps {
         
        sh "mvn clean package" 
        
        }
     }
     
     stage ('Sonar-Report') {
         steps {
             sh "mvn clean sonar:sonar"
         }
     }
     
     stage ('Deploy to Nexus') {
         steps {
             sh "mvn clean deploy"
         }
     }
     
     stage ('Deploy to Tomcat') {
         steps {
             sh """
             curl -u shiva:shiv123 \
                --upload-file /var/lib/jenkins/workspace/maven-DPL/target/maven-web-application.war \
                "http://54.197.173.161:9090/manager/text/deploy?path=/maven-web-application&update=true"
             """
         }
     }
     
    } // stages close
} // pipline close
