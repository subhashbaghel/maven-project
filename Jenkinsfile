pipeline {
    agent any
    tools { 
        jdk 'java8'
        maven 'maven3.39'
    }
        stages {
            stage ('Build') {
                steps {
                    echo "This is Build "
                    sh label: '', script: '''mvn clean package checkstyle:checkstyle'''
                                    
                            }
                            post {
                                success {
                                    echo "Archive Artifacts"
                                    archive '**/*.war'
                                    echo "Publish Junit Report"
                                    junit '**/target/surefire-reports/*.xml'
                                    echo " Publish checkstyle Report"
                                    checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
                                }
                            }
            }
            stage ('Deploy-test') {
                steps {
                    echo "This is Deploy-test"
                    build 'java-deploy'
                }
            }
            stage ('Producation') {
                steps {
                    echo "This is Producation"
                    timeout(time: 60, unit: 'SECONDS' {
                        input 'do you want to deploy  ?'
                    }
                    build 'dev-test'
                }
            }
        }
}
