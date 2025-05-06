Configure a job to run on a node
--
Dashboard -- javaapp -- Configuration -- general
select "Restrict where this project can be run"
Label Expression: linux

save

build with parameter

Update the pipeline to run the job on linux node
----

pipeline {
    agent {
        label 'linux'
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MVN3"
    }

    stages {
        stage('pull scm') {
            steps {
                // Get some code from a GitHub repository
                git credentialsId: 'github', url: 'git@github.com:deviprasadkk/jenkins_test.git'
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true -f api-gateway/ clean package"
            }
                            
        }
        
        stage('archive') {
            steps {
                archiveArtifacts artifacts: 'api-gateway/target/*.jar', followSymlinks: false
            }
        }
        
        stage('publish test result') {
            steps {
                junit 'api-gateway/target/surefire-reports/*.xml'
            }
        }
        
        stage('test') {
            steps {
                sh "echo testing"
            }
        }
    }
}
