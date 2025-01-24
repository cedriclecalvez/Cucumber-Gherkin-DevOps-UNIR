pipeline {
    agent any
    
    stages {
      
        stage('Get Code') {
            steps {
                bat 'dir'
                bat 'echo %WORKSPACE%'
                git url: 'https://github.com/cedriclecalvez/Cucumber-Gherkin-DevOps-UNIR'
				
            }
        }
        
        stage('Build&Test')
        {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    bat 'cd \\wsl.localhost\\Ubuntu-20.04\\usr\\share\\maven\\bin && mvn test'
                }
            }
        }
        
        stage('Results')
        {
            steps {
                cucumber fileIncludePattern: 'cucumber.json', jsonReportDirectory: 'target/', reportTitle: 'Cucumber Reports',failedScenariosNumber:1, buildStatus:'FAILURE'
            }
        }
    }
}		