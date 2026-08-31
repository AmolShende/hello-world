pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/AmolShende/hello-world.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy(
                    adapters: [
                        tomcat9(
                            credentialsId: 'tomcat_credential',
                            path: '',
                            url: 'http://172.31.7.88:8090'
                        )
                    ],
                    contextPath: '/hello-world',
                    war: '**/*.war'
                )
            }
        }
    }
}
