pipeline {
    agent any
    tools { 
        jdk 'java8'
        maven 'maven3.39'
    }
        stages {
            stage ('Build') {
                steps {
                    echo "This is Build"
                    sh label: '', script: '''mvn clean package'''
                                    
                            }
                            post {
                                success {
                                    echo "Archive Artifacts"
                                    archive '**/*.war'
                                    echo "Publish Junit Report"
                                    sh label: '', script: '''**/target/surefire-reports/*.xml'''
                                    echo " Publish checkstyle Report"
                                    sh label: '', script: '''checkstyle:checkstyle'''
                                }
                            }
            }
            stage ('Deploy-test') {
                steps {
                    echo "This is Deploy-test"
                }
            }
            stage ('QA') {
                steps {
                    echo "This is QA"
                }
            }
        }
}
