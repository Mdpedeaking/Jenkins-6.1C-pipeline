pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo "-Fetch the source code from the directory path specified by the environment variable-"
                    echo "-Compile and package the code using Gradle-"
                    echo "Within the build stage, the code is compiled and packaged into a deployable artifact where the foundations of the next stages are set." 
                    echo "It is within this step that ensures that commits pushed through to the git repository goes through consistently and repeatedly, so that errors can be caught early in the development cycle to facilitate the continuous and integrated delivery."
                    echo "Throughout this pipeline, I recommend using gradle, which is an automation tool that handles project dependencies and conveniently compiles and runs tests on the code and packages the application"
                    // sh 'gradle clean build' -> sample command to compile and package the code using gradle
                }
            }
            post {
                always {
                    script {
                        emailext attachLog: true, 
                                 subject: "Build STATUS - ${currentBuild.currentResult}", 
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
                    echo "Within this stage, the pipeline ensures that the code will function correctly while integrating well with the other possible components."
                    echo "In this stage, unit tests and integration tests are run on individual components (units) of the code, to verify functionality and reliability of the code and overall application and that services within the application are well integrated."
                    // sh 'gradle test' -> command to test the code using gradle
                    // sh "gradle integrationTest" -> command to integrate the tested code using gradle
                }
            }
            post {
                always {
                    script {
                        emailext attachLog: true, 
                                 subject: "Unit and Integration Tests STATUS - ${currentBuild.currentResult}", 
                                 body: "Unit and Integration tests have ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    echo "Code Analysis: Analyse the code using PMD gradle configurations"
                    echo "Within this stage, it is ensured that the code meets industry standards and identifies potential coding violations (style or copyright for example), and other potential bugs."
                    echo "PMD (programming mistake detector) is used through gradle configurations into the pipeline to identify such problematic patterns within the main source code of the project early in the development process."
                    // sh 'gradle pmdMain' -> command to analyse the code using gradle PMD configurations
                }
            }
            post {
                always {
                    script {
                        emailext attachLog: true, 
                                 subject: "Code Analysis STATUS - ${currentBuild.currentResult}", 
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
                    echo "Within this stage, potential vulnerabilities are identified in the project's dependencies using this tool within the libraries and its code components."
                    // dependencyCheck additionalArguments: '--project "your-project" --scan .', odcInstallation: 'Dependency-Check' -> command for the security scan using OWASP Dependency-Check plugin
                }
            }
            post {
                always {
                    script {
                        emailext attachLog: true, 
                                 subject: "Security Scan STATUS - ${currentBuild.currentResult}", 
                                 body: "Security scan has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploy to Staging: Deploy the application to a staging server"
                    echo "Within this stage, the SSH method is configured within Gradle to automate the deployment process to a staging environment, to verify that the application functions and artifacts work well in a production-like setting before releasing it to the production stage of the pipeline"
                    // sshagent(credentials: [env.SSH_CREDENTIALS_ID]) {
                    //     sh """
                    //     scp -o StrictHostKeyChecking=no build/libs/your-app.jar user@${env.STAGING_SERVER}:/path/to/deploy/
                    //     ssh -o StrictHostKeyChecking=no user@${env.STAGING_SERVER} 'bash -s' < deploy_script.sh
                    //     """
                    // } -> staging server reached through referencing potential environment variables that could be created for the staging server
                }
            }
            post {
                always {
                    script {
                        emailext attachLog: true, 
                                 subject: "Deployment to Staging STATUS - ${currentBuild.currentResult}", 
                                 body: "Deployment to staging has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Integration Tests on Staging: Run integration tests within the staging environment"
                    echo "Within this stage, using gradle configurations to automate the execution of integration tests, the application behavior can be verified that it works as expected in a real-world scenario."
                    echo "It identifies any issues that may arise within environment-specific configurations or interactions with external systems."
                    // sh 'gradle integrationTest' -> integration testing within the staging environment using gradle configurations
                }
            }
            post {
                always {
                    script {
                        emailext attachLog: true, 
                                 subject: "Integration Tests on Staging STATUS - ${currentBuild.currentResult}", 
                                 body: "Integration tests on staging have ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploy to Production."
                    echo "Deploy the application to a production server on Google Cloud computing engine using Gradle SSH configurations within Jenkins."
                    echo "Automation of this stage ensures consistency and reliability of the deployment"
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
                        emailext attachLog: true, 
                                 subject: "Deployment to Production STATUS - ${currentBuild.currentResult}", 
                                 body: "Deployment to production has ${currentBuild.currentResult}.",
                                 to: 'nethmini2020.p@gmail.com'
                    }
                }
            }
        }
    }
}

