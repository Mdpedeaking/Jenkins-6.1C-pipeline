pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo "Fetch the source code from the directory path specified by the environment variable"
                    echo "Compile and package the code using Gradle"
                    // sh 'gradle clean build' -> command to compile and package the code using gradle
                }
            }
            post {
                always {
                    script {
                        def logFileName = "build-log-${env.BUILD_TAG}.txt"
                        sh "cp ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log ${WORKSPACE}/${logFileName}"
                        emailext attachLog: false, 
                                 attachmentsPattern: logFileName, 
                                 subject: "Build Status - ${currentBuild.currentResult}", 
                                 body: "Gradle build has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo "Unit and Integration Tests: Run unit tests and integration tests using JUnit gradle tests and integration test"
                    // sh 'gradle test' -> command to test the code using gradle
                    // sh "gradle integrationTest" -> command to integrate the tested code using gradle
                }
            }
            post {
                always {
                    script {
                        def logFileName = "unit-integration-tests-log-${env.BUILD_TAG}.txt"
                        sh "cp ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log ${WORKSPACE}/${logFileName}"
                        emailext attachLog: false, 
                                 attachmentsPattern: logFileName, 
                                 subject: "Unit and Integration Tests Status - ${currentBuild.currentResult}", 
                                 body: "Unit and Integration tests have ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    echo "Code Analysis: Analyse the code using PMD gradle configurations to ensure it meets industry standards"
                    // sh 'gradle pmdMain' -> command to analyse the code using gradle PMD configurations
                }
            }
            post {
                always {
                    script {
                        def logFileName = "code-analysis-log-${env.BUILD_TAG}.txt"
                        sh "cp ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log ${WORKSPACE}/${logFileName}"
                        emailext attachLog: false, 
                                 attachmentsPattern: logFileName, 
                                 subject: "Code Analysis Status - ${currentBuild.currentResult}", 
                                 body: "Code analysis has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    echo "Security Scan: Perform a security scan using OWASP Dependency-Check to identify vulnerabilities"
                    // dependencyCheck additionalArguments: '--project "your-project" --scan .', odcInstallation: 'Dependency-Check' -> command for the security scan using OWASP Dependency-Check plugin
                }
            }
            post {
                always {
                    script {
                        def logFileName = "security-scan-log-${env.BUILD_TAG}.txt"
                        sh "cp ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log ${WORKSPACE}/${logFileName}"
                        emailext attachLog: false, 
                                 attachmentsPattern: logFileName, 
                                 subject: "Security Scan Status - ${currentBuild.currentResult}", 
                                 body: "Security scan has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploy to Staging: Deploy the application to a staging server using the SSH method in gradle configurations"
                    // sshagent(credentials: [env.SSH_CREDENTIALS_ID]) {
                    //     sh """
                    //     scp -o StrictHostKeyChecking=no build/libs/your-app.jar user@${env.STAGING_SERVER}:/path/to/deploy/ ->
                    //     ssh -o StrictHostKeyChecking=no user@${env.STAGING_SERVER} 'bash -s' < deploy_script.sh
                    //     """
                    // } -> staging server reached through referencing potential environment variables that could be created for the staging server
                }
            }
            post {
                always {
                    script {
                        def logFileName = "deploy-to-staging-log-${env.BUILD_TAG}.txt"
                        sh "cp ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log ${WORKSPACE}/${logFileName}"
                        emailext attachLog: false, 
                                 attachmentsPattern: logFileName, 
                                 subject: "Deployment to Staging Status - ${currentBuild.currentResult}", 
                                 body: "Deployment to staging has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Integration Tests on Staging: Run integration tests within the staging environment using gradle configurations"
                    // sh 'gradle integrationTest' -> integration testing within the staging environment using gradle configurations
                }
            }
            post {
                always {
                    script {
                        def logFileName = "integration-tests-on-staging-log-${env.BUILD_TAG}.txt"
                        sh "cp ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log ${WORKSPACE}/${logFileName}"
                        emailext attachLog: false, 
                                 attachmentsPattern: logFileName, 
                                 subject: "Integration Tests on Staging Status - ${currentBuild.currentResult}", 
                                 body: "Integration tests on staging have ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploy to Production: Deploy the application to a production server on google cloud computing engine"
                    // sshagent(credentials: [env.SSH_CREDENTIALS_ID]) {
                    //     sh """
                    //     scp -o StrictHostKeyChecking=no build/libs/your-app.jar user@${env.PRODUCTION_SERVER}:/path/to/deploy/
                    //     ssh -o StrictHostKeyChecking=no user@${env.PRODUCTION_SERVER} 'bash -s' < deploy_script.sh
                    //     """
                    // } -> deploying to the production server reached through referencing potential environment variables that could be created for the production server
                }
            }
            post {
                always {
                    script {
                        def logFileName = "deploy-to-production-log-${env.BUILD_TAG}.txt"
                        sh "cp ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log ${WORKSPACE}/${logFileName}"
                        emailext attachLog: false, 
                                 attachmentsPattern: logFileName, 
                                 subject: "Deployment to Production Status - ${currentBuild.currentResult}", 
                                 body: "Deployment to production has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
    }
}

