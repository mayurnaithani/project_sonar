pipeline{

      agent any
        
        stages{

              stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('sonarserver') { 
				  withMaven(maven: 'maven3') {
			      sh "mvn clean install"
			      //sh "mvn jacoco:prepare-agent"
			      //sh "mvn jacoco:report"
			      sh "mvn sonar:sonar -Dsonar.projectKey=test-project"
				 }
				}
			      timeout(time: 1, unit: 'HOURS') {
			      def qg = waitForQualityGate()
				      if (qg.status != 'OK') {
					   error "Pipeline aborted due to quality gate failure: ${qg.status}"
				      }
                    		}
		    	     //sh "mvn clean install"
		  
                 	}
               	 }  
              }	
		
            }	       	     	         
}
