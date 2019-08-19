pipeline {
    agent any

    environment {
        
         PROJECT_KEY = 'soanr_qube_qualitygates'
         PROJECT_NAME= 'calculation'
         testcoverage = 'testcoverage'
      
    }

    stages {        
        stage('Clone git') {
            steps {
               git 'https://github.com/bisap/Docker-Jenkins-SonarQube-NETCore-V1.git'
            }
        }    

       stage('dotnet test') {
            steps {        

     def sqScannerMsBuildHome = tool 'Scanner for MSBuild 4.6'
      withSonarQubeEnv('My SonarQube Server') {
          
      bat "${sqScannerMsBuildHome}\\SonarQube.Scanner.MSBuild.exe begin /k:soanr_qube_qualitygates"
      bat 'MSBuild.exe /t:Rebuild'
      bat "${sqScannerMsBuildHome}\\SonarQube.Scanner.MSBuild.exe end"
            //  //  sh "dotnet tool install --global coverlet.console --version 1.4.1"
            // sh "dotnet restore"
            // sh "dotnet test calculation.tests/calculation.tests.csproj --logger:\"trx;LogFileName=testresult.xml\"  /p:CollectCoverage=true /p:CoverletOutputFormat=opencover  /p:CoverletOutput=\"TestResults\\opencover.xml\"" 
            // sh "dotnet build-server shutdown"
            // sh "dotnet sonarscanner begin /k:\"soanr_qube_qualitygates\" /d:sonar.host.url=http://139.59.47.153:9000 /d:sonar.cs.opencover.reportsPaths=\"**/TestResults/opencover.xml\"  /d:sonar.cs.vstest.reportsPaths=\"**/TestResults/testresult.xml\"   /d:sonar.scm.disabled=true /d:sonar.coverage.dtdVerification=true  /d:sonar.coverage.exclusions=\"*Tests*.cs,*testresult*.xml,*opencover*.xml\"  /d:sonar.test.exclusions=\"*Tests*.cs,*testresult*.xml,*opencover*.xml\" "
            // sh "dotnet build"
            // sh "dotnet sonarscanner end"
 
            }
        }
    }
}