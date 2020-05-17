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

                
        
                // stage('Run_Security_Scanning'){
                //     steps {
                //         script {
                //             sh "echo 'Security Scanning'"
                //             sh '''
                //             curl -XPOST -H "Authorization: token $GITHUB_TOKEN" $GITHUB_API_URL/$REPO_OWNER_NAME/$REPO_NAME/statuses/$(git rev-parse HEAD) -d '{"state": "pending","context":"ci/jenkins: run-sonarqube", "target_url": $JENKINS_URL,"description": "Your tests are queued behind your running builds!"}'
                //             '''

                //             def scannerhome = tool 'SonarQubeScanner';
                //             withSonarQubeEnv('SonarQube') {      
                //             sh 'mvn sonar:sonar -Dsonar.projectKey=${SONAR_PROJECT_NAME} -Dsonar.login=${SONAR_TOKEN}'
                //             sh 'rm -rf sonarqubereports  || echo "directory does not exist"'
                //             sh 'mkdir sonarqubereports'
                //             sh 'sleep 5'
                //             sh 'wget https://github.com/lequal/sonar-cnes-report/releases/download/3.1.0/sonar-cnes-report-3.1.0.jar'
                //             sh 'java -jar ./sonar-cnes-report-3.1.0.jar -t ${SONAR_TOKEN} -s ${SONAR_HOST} -p ${SONAR_PROJECT_NAME} -o sonarqubereports'
                //             sh 'cp sonarqubereports/*-BossAPI-analysis-report.docx sonarqubereports/sonarqubeanalysisreport.docx'
                //             sh 'cp sonarqubereports/*-BossAPI-issues-report.xlsx sonarqubereports/sonarqubeissuesreport.xlsx'
                //                 archiveArtifacts artifacts: 'sonarqubereports/sonarqubeanalysisreport.docx', fingerprint: true
                //                 archiveArtifacts artifacts: 'sonarqubereports/sonarqubeissuesreport.xlsx', fingerprint: true
			    
                //             sh  '''
                //                 curl -XPOST -H "Authorization: token $GITHUB_TOKEN" $GITHUB_API_URL/$REPO_OWNER_NAME/$REPO_NAME/statuses/$(git rev-parse HEAD) -d '{"state": "pending","context":"ci/jenkins: run-sonarqube", "target_url": $JENKINS_URL,"description": "Your tests are queued behind your running builds!"}'
                //                 '''			    
		        //                     RUN_SECURITY_SCAN_STATUS= 'Success'

                //                 // timeout(time: 2, unit: 'MINUTES') {
                //                 //         waitForQualityGate abortPipeline: false
                            
                            
                //                 // }
                //             }
                //         }
                //     }
                //     post {
                //         failure {
                //             script {
        		//             RUN_SECURITY_SCAN_STATUS= 'Failed'
                //                 sh '''
                //                 curl -XPOST -H "Authorization: token $GITHUB_TOKEN" $GITHUB_API_URL/repos/$REPO_OWNER_NAME/$REPO_NAME/$(git rev-parse HEAD) -d "{'state': 'failure','context':'ci/jenkins: run-sonarqube', 'target_url': JENKINS_URL,'description': 'Your tests failed on Jenkins!'}"
                //                 '''				       
        	   	//                 sh 'echo "FAILED in stage SonarQube"'
    		    //             }
                //         }
                //     }	
                // }

                

                                
                
        }
        
    
        
}