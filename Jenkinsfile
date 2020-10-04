pipeline{

      agent any
        
        stages{

              stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('sonarserver') { 
				  withMaven(maven: 'maven3') {
			      sh "mvn clean jacoco:prepare-agent install -Dmaven.test.failure.ignore=false"
			      sh "mvn jacoco:report"
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
