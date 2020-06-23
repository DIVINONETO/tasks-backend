pipeline {
    agent any
    stages {
        stage("Build Backend") {
            steps {
                bat "mvn clean package -DskipTests=true"
            }
        }
        stage("Unit Tests") {
            steps {
                bat "mvn test"
            }
        }
        stage ("Deploy Backend") {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'Tomcat', path: '', url: 'http://127.0.0.1:8009/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }
    }
}