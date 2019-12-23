 
node{
 
  def mvnHome 
  
   stage('Git Checkout') 
     {    
          // Get some code from a GitHub repository.
      
             git 'https://github.com/shubhamselenium/POM'
    
          // Get the Maven tool.
      
             mvnHome = tool 'Maven_3.6.2'
                
      }
    stage('Code Analysis')
            {

              echo "Analyzing the code"
              
            }
   
    stage('Unit Testing')
          {
            
             echo 'Performing Unit Testing'
           
          }
    
    
    stage('Integrationn Testing')
         {
          
              echo 'Performing Integrationn Testing'
          
         }
    
   stage('System Testing')
         {
           
             echo'Performing System Testing'
          
         }
   
    stage('System Release') 
         {
           // Run the maven build
            withEnv(["MVN_HOME=$mvnHome"]) 
              {
               if (isUnix()) 
                  {
                    
                     sh '"$MVN_HOME/bin/mvn"  package'
                  } 
               else 
                  {
                     bat(/"%MVN_HOME%\bin\mvn" package/)
                  }
              }
          }
   
 
   stage('Result : Report')
   {
    
            publishHTML(target:[allowMissing: false, 
                       alwaysLinkToLastBuild: false, 
                       keepAll: true, 
                       reportDir: 'test-output', 
                       reportFiles: 'ExtentReposhot.html', 
                       reportName: 'Piplined HTML Report', 
                       reportTitles: 'Pipeline Job'])

    }   

   
   

   stage ('Email : Alert Notification')
   {
     
      mail bcc: '', 
           body: '''This is Jenkins job''', 
           cc: '', 
           from: '', 
           replyTo: "javaselenium681@gmail.com", 
           subject: "This is DeclarativePipeline Job..${currentBuild.fullDisplayName}", 
           to: "javaselenium681@gmail.com"
 
   }
   
   stage('Email : Report Notification')
   {
         
          emailext body: "${SCRIPT, template='regressionfailed.groovy'}",
                 attachmentsPattern: '**/*.html',
                 subject: "This is DeclarativePipeline Job Status,,${currentBuild.fullDisplayName} ${env.JOB_NAME} - Build# ${env.BUILD_NUMBER} - ${env.BUILD_STATUS}",
                 to: "javaselenium681@gmail.com",
                 replyTo: "javaselenium681@gmail.com",
                 attachLog: true,  
                 compressLog: true
   }
 
      stage('Trigger Schedul : Job ')
           {
            
                 cron('H */4 * * 1-5')
           
           }

  
  }
     

