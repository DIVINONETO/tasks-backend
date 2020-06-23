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
         stage("Deploy Frontend") {
            steps {
                dir("frontend") {
                    git credentialsId: 'github_login', url 'https://github.com/DIVINONETO/tasks-frontend'
                    bat "mvn clean package"
                    deploy adapters: [tomcat8(credentialsId: 'Tomcat', path: '', url: 'http://127.0.0.1:8009/')], contextPath: 'tasks', war: 'target/tasks.war'

                }
            }
        }
    }
}