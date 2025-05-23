pipeline {
    agent any
    stages {
        stage('clean_workspace') {
            steps {
                // You can choose to clean workspace before build as follows
                cleanWs deleteDirs: true, notFailBuild: true
                checkout scm
               
            }
        }
        
        stage ('Build') {
            steps { 
                    sh 'mvn clean install -DskipTests=true '                                    
               }
         }
        
                   
    }
}

pipeline {
    agent any
    parameters {
    booleanParam(name: 'BUILD_APP', defaultValue: true, description: 'Build the application?')
    booleanParam(name: 'DEPLOY_APP', defaultValue: true, description: 'Deploy the application?')
    string(name: 'DEPLOY_VERSION', defaultValue: '', description: 'Custom version to deploy (leave blank to use build number)')
    }

    environment {
        APP_NAME= 'demo-consumer-service'
        APP_DEPLOY_NAME= 'demo-consumer-service'
        DEPLOYMENT_GROUP_NAME = "demo-consumer-service-dg"
        AWS_REGION = "us-east-2"
        S3_BUCKET_NAME = "demo-build-artifcats"
        ARTIFACT_KEY = "${JOB_NAME}/${DEPLOY_VERSION ?: env.BUILD_NUMBER}/${APP_NAME}.zip"
	SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_AUTH_TOKEN = credentials('sonar-qube-key')  // Store SonarQube token in Jenkins Credentials
        SONAR_PROJECT_KEY = 'security-monitoring-consumer-service'
        SONAR_PROJECT_NAME = 'security-monitoring-consumer-service'
    }
    // tools {
    //     maven 'Maven-3'
    // }
    stages {
        stage('review parameters') {
            steps {
                echo "Deploy version is: ${params.DEPLOY_VERSION}"
                echo "Build number is: ${env.BUILD_NUMBER}"
            }
        }
        stage('Build') {
            when {
                expression { params.BUILD_APP }
            }
            steps {

                sh 'mvn clean install -Dspring.profiles.active=prod'
            }
        }

       
    }
  
}
