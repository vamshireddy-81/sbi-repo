node{

   def tomcatWeb = 'C:\\Devops\\Software\\apache-tomcat-10.1.1\\webapps'
   def tomcatBin = 'C:\\Devops\\Software\\apache-tomcat-10.1.1\\bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/vamshireddy-81/sbi-repo.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'Maven', type: 'maven'   
      bat "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     bat "copy target\\CICDPipeline.war \"${tomcatWeb}\\CICDPipeline.war\""
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.bat"
         sleep(time:100,unit:"SECONDS")
   }
}
