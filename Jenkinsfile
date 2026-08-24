//qa jenkins pipeline
pipeline
{
    
   agent any
   tools
   {
      maven "maven-3.9.6"
   }
   stages
   {
           stage('git checkout')
           {
              steps
              {
                 
                 git branch: 'qa', url: 'https://github.com/Sunilg3377/maven-webapplication.git'
              }
           }
           stage('compile')
           {
              steps
              {
                 sh "mvn compile"
              }
           }
           stage('Build')
           {
             steps
             {
               sh "mvn clean package"
             }
           }
         stage('SQ REPORT')
           {
             steps
             {
                sh "mvn sonar:sonar"
             }
           }   
           stage('Deploy to nexus')
           {
              steps
              {
                sh "mvn clean deploy"
              }
           }
           stage('Deploy to tomcat')
           {
              steps
              {
                 sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/jio-Declarative-PL-dev/target/maven-web-application.war \
"http://100.25.246.255:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
              }
           }
           stage ('bsnl-uat')
           {
             steps
              {
                build job: 'bsnl-uat'
              }
            } 
   } //pipeline ending
