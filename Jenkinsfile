def gv
pipeline{
    agent any
     parameters {
	choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
	booleanParam(name: 'executeTests', defaultValue: false, description: '')
    }						
    stages{
        stage ("init"){
             steps {
		 script {
		      gv = load "script.groovy"
			}
            }
            
        }

	stage ("build"){
             steps {
		script {
			gv.buildApp()
            }
	  }
	}
        stage ("test"){
	when {
	        expression {
			params.executeTests
	}
	    }
             steps {
               script {
			gv.testApp()
            }
            }
            
        }
        stage ("Deploy"){
	    input{
		message "Select the environment to deploy to"
		ok "Done"
		parameters{
			choice(name: 'ENVIRONMENT', choices: ['DEV', 'STAGING', 'PRODUCTION'], description: '')
		}
		    
	    }
             steps {
                script {
			gv.deployApp()
			echo "Deploying to ${ENVIRONMENT}"
            }
            }        
        }
    }
}
