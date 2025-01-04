@Library('my-shared-library@main') _

pipeline {
    agent { label 'server1' }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps { 
                script {
                   pipelineAll.checkoutCode()
               }
            }
        }

        stage('Set up Java 17') {
            steps {
                 script {
                   pipelineAll.setupJava()
                 }
            }
        }

        stage('Set up Maven') {
            steps {
                 script {
                   pipelineAll.setupMaven()
                 }
            }
        }

        stage('Build with Maven') {
            steps {
                 script {
                   pipelineAll.buildProject()
                 }
            }
        }
        
        stage('Upload Artifact') {
            steps {
                 script {
                   pipelineAll.uploadArtifact('target/petclinic-0.0.1-SNAPSHOT.jar')
                 }
            }
        }

        stage('Run Application') {
            steps {
                 script {
                   pipelineAll.runApplication()
                 }
            }
        }

        stage('Validate App is Running') {
            steps {
                 script {
                   pipelineAll.validateApp()
                 }
            }
        }

        stage('Gracefully Stop Spring Boot App') {
            steps {
                 script {
                   pipelineAll.stopApplication()
                 }
            }
        }
    }

    post {
        always {
             script {
                   pipelineAll.cleanup()
             }
        }
    }
}
