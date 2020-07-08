pipeline{
    
    tools{
       
        maven 'Mymaven'
    }
    agent none
    stages{
        stage('Checkout'){
            agent any
            steps{
            git 'https://github.com/prudhvi34/DevOpsClassCodes.git'
            }
        }
        stage('compile'){
            agent any
            steps{
                sh 'mvn compile'
            }
        }
        stage('codeReview'){
            agent any
            steps{
                sh 'mvn pmd:pmd'
            }
            post{
                always{
                    pmd pattern: 'target/pmd.xml'
                }
            }
            
        }
        stage('unitTest'){
            agent any
            steps{
               sh 'mvn test'
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('MetricCheck'){
            agent any
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post{
                always{
                    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                }
            }
        }
        stage('package'){
            agent any
            steps{
                sh 'mvn package'
            }
        }
    }
}
