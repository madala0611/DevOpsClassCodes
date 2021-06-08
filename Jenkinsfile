pipeline{
    tools{
        jdk 'MyLocalJava'
        maven 'MyLocalMaven'
    }
    agent any
    stages{
        stage('Clone Repo'){
            steps{
                git 'https://github.com/madala0611/DevOpsClassCodes.git'
            }
        }
        stage('Compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Code Review'){
            steps{
                sh 'mvn pmd:pmd'
            }
        }
        stage('Unit Test'){
            steps{
		agent label{win_slave}
		git 'https://github.com/madala0611/DevOpsClassCodes.git'
                bat 'mvn test'
            }
	    post{
               success {
                   junit 'target/surefire-reports/*.xml'
               }
			}
        }
        stage('Code Coverage'){
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
	    post{
               success {
	           cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false                  
               }
			}
        }
        stage('Package'){
            steps{
                sh 'mvn package'
            }
        }
        
    }
}
