pipeline
{
    parameters {
		booleanParam(defaultValue: false, description: 'To check the Production or Non-Production', name: 'check_condition')
    }
	agent any
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
           powershell '''
				Write-Host "CONDITION: $check_condition"
				if ( $check_condition ) {
				  Write-Host "No String Replace"
				}
				else {
				Write-Host "Replace String"
				(Get-Content '$WORKSPACE\\space folder\\main.py') -replace 'sfdcSandbox = True', 'sfdcSandbox = False' | Out-File -encoding ASCII '$WORKSPACE\\space folder\\main.py'
				}
              '''
          }
      }
  }
}
