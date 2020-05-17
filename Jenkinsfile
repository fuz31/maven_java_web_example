pipeline {
    agent {
        node {
            label 'linux-worker-1'
        }
    }  


    stages {     
        stage('Checkout from SCM'){
            steps {
                git 'https://github.com/fuz31/maven_java_web_example.git'
            }

            
        }   

        stage('Build Application'){
            steps {
                script {
                    sh 'mvn clean compile verify'
                }

               
             }

         }

                
        
                stage('Run_Security_Scanning'){
                    steps {
                        script {
                            

                            def scannerhome = tool 'cynerge-sonarqube';
                            withSonarQubeEnv() {      
                            sh 'mvn sonar:sonar -Dsonar.projectName=Cynerge-Demo -Dsonar.projectKey=Cynerge-Demo -Dsonar.host.url=http://3.221.118.166 -Dsonar.login=8f1b7aace3c4980743fac4682947df2f28be34be'
                            sh 'rm -rf sonarqubereports  || echo "directory does not exist"'
                            sh 'mkdir sonarqubereports'
                            sh 'sleep 5'
                            sh 'wget https://github.com/lequal/sonar-cnes-report/releases/download/3.1.0/sonar-cnes-report-3.1.0.jar'
                            sh 'java -jar ./sonar-cnes-report-3.1.0.jar -t 8f1b7aace3c4980743fac4682947df2f28be34be -s http://3.221.118.166 -p Cynerge-Demo -o sonarqubereports'
                            sh 'cp sonarqubereports/*-Cynerge-Demo-analysis-report.docx sonarqubereports/sonarqubeanalysisreport.docx'
                            sh 'cp sonarqubereports/*-Cynerge-Demo-issues-report.xlsx sonarqubereports/sonarqubeissuesreport.xlsx'
                                archiveArtifacts artifacts: 'sonarqubereports/sonarqubeanalysisreport.docx', fingerprint: true
                                archiveArtifacts artifacts: 'sonarqubereports/sonarqubeissuesreport.xlsx', fingerprint: true
			    


                                // timeout(time: 2, unit: 'MINUTES') {
                                //         waitForQualityGate abortPipeline: false
                            
                            
                                // }
                            }
                        }
                    }
                }

                stage('Selenium tests'){
                    stages{
                        stage('Checking out selenium code'){
                            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/fuz31/automated-functional-tests.git']]])
                        }

                        stage('Execute selenium code'){
                            steps{
                                sh 'ls'
                                nodejs('Node14') {
                                    npm verison
                            }
                        }
                        }
                    }
                }  
                    // post {
                    //     failure {
                    //         script {
        		    //         RUN_SECURITY_SCAN_STATUS= 'Failed'
                    //             sh '''
                    //             curl -XPOST -H "Authorization: token $GITHUB_TOKEN" $GITHUB_API_URL/repos/$REPO_OWNER_NAME/$REPO_NAME/$(git rev-parse HEAD) -d "{'state': 'failure','context':'ci/jenkins: run-sonarqube', 'target_url': JENKINS_URL,'description': 'Your tests failed on Jenkins!'}"
                    //             '''				       
        	   	    //             sh 'echo "FAILED in stage SonarQube"'
    		        //         }
                    //     }
                    // }	
                }

                

                                
                
        }
        
    
        
}