pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is available in the workspace'
            }
        }

        stage('Maven Test') {
            steps {
                sh 'export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 && export PATH="$JAVA_HOME/bin:$PATH" && mvn clean test'
            }
        }

        stage('Package') {
            steps {
                sh 'export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 && export PATH="$JAVA_HOME/bin:$PATH" && mvn package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t campus-equipment-booking:set-e .'
            }
        }
    }
}
