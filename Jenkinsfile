pipeline {
    agent any
    tools {
        maven 'Maven-3.9'
    }
    stages {
        stage('1. Checkout Code') {
            steps {
                echo 'Fetching source code from GitHub...'
                checkout scm
            }
        }
        stage('2. Build') {
            steps {
                echo 'Compiling the Java application...'
                sh 'mvn clean compile'
            }
        }
        stage('3. Unit Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
                }
            }
        }
        stage('4. Package') {
            steps {
                echo 'Packaging application into JAR...'
                sh 'mvn package -DskipTests'
            }
        }
        stage('5. Deploy') {
            steps {
                echo 'Deploying application artifact...'
                sh '''
                    cp target/my-java-app.jar /tmp/deployed-app.jar
                    ls -l /tmp/deployed-app.jar
                    echo "Deployment completed successfully."
                '''
            }
        }
    }
    post {
        success { echo 'Pipeline completed successfully!' }
        failure { echo 'Pipeline failed. Check the logs for details.' }
    }
}
