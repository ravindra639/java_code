pipeline
{
    parameters {
		booleanParam(defaultValue: false, description: 'To check the Production or Non-Production', name: 'check_condition')
    }
	environment {
        EMAIL_RECIPIENTS   = "${TA_MAIL}"
    }
    options {
    disableConcurrentBuilds()
	timestamps()
    }
  //agent { label 'hsdp_ci_ciforci' }
  stages {
      stage ('Deploy')
      {
          steps {
           bat '''
				@echo off
				echo %check_condition%
				if %check_condition%=False
				powerhsell (Get-Content '$WORKSPACE\\space folder\\main.py') -replace 'sfdcSandbox = True', 'sfdcSandbox = False' | Out-File -encoding ASCII '$WORKSPACE\\space folder\\main.py'
				else
				echo "No string Replace is required"
              '''
          }
      }
  }
}
