node {
  stage('SCM') {
    git 'https://github.com/bisap/Docker-Jenkins-SonarQube-NETCore-V2.git'
  }
  stage('Build + SonarQube analysis') {
    // def sqScannerMsBuildHome = tool ' SonarScanner for MSBuild 4.6.2.2108'
    withSonarQubeEnv('devops') {
             sh "dotnet restore"
            sh "dotnet test calculation.tests/calculation.tests.csproj --logger:\"trx;LogFileName=testresult.xml\"  /p:CollectCoverage=true /p:CoverletOutputFormat=opencover  /p:CoverletOutput=\"TestResults\\opencover.xml\"" 
            sh "dotnet build-server shutdown"
            sh "dotnet sonarscanner begin /k:\"soanr_qube_qualitygates\" /d:sonar.host.url=http://139.59.47.153:9000 /d:sonar.cs.opencover.reportsPaths=\"**/TestResults/opencover.xml\"  /d:sonar.cs.vstest.reportsPaths=\"**/TestResults/testresult.xml\"   /d:sonar.scm.disabled=true /d:sonar.coverage.dtdVerification=true  /d:sonar.coverage.exclusions=\"*Tests*.cs,*testresult*.xml,*opencover*.xml\"  /d:sonar.test.exclusions=\"*Tests*.cs,*testresult*.xml,*opencover*.xml\" "
            sh "dotnet build"
            sh "dotnet sonarscanner end"
    }
  }

   stage("Quality Gate Statuc Check"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {                 
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }    
}