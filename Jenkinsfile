pipeline {
    agent {
        label "jenkins-node"
    }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/c1t1d0s7/mywebapp'
            }
        }
        stage('Maven Build') {
            steps {
                sh ' mvn package -Dmaven.test.skip=true'
            }
        }
        stage('Maven Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Tomcat Deploy') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-manager', 
                        path: '', url: 'http://192.168.56.102:8080'
                    )
                ], 
                contextPath: null, 
                war: 'target/hello-world.war'
            }
        }
    }
}
