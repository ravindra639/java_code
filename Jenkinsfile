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
  stages {
      stage ('Deploy')
      {
          steps {
           powershell '''
				if($check_condition) {
				  Write-Host "No String Replace"
				}
				else {
				Write-Host "Replace String"
				(Get-Content 'space folder\\main.py') -replace 'sfdcSandbox = True', 'sfdcSandbox = False' | Out-File -encoding ASCII 'space folder\\main.py'
				}
              '''
          }
      }
  }
}
