currentBuild.displayName = "DevOps-prushi-#"+currentBuild.number
pipeline {
    agent {
        label '!master'
    }
        environment {
            PATH = "/usr/local/src/apache-maven/bin/:$PATH"
    }
    stages {
        stage ('test') {
            steps {
                git url: "https://github.com/javahometech/myweb.git"
            }
        }
        stage ('maven-build') {
            steps {
                sh '''
                mvn clean package
                mv target/*.war target/mywebapp.war
                '''
            }
        }
        stage ('tomcat-host') {
            steps {
                sh '''
                cp -rvf target/mywebapp.war /opt/apache-tomcat/webapps/
                '''
            }
        }
        stage ('docker') {
            steps {
                sh 'docker build -t mywebapp .'
            }
        }
    }
}