pipeline {
    agent any
    environment {
        M2_HOME='/opt/apache-maven-3.9.5'
        PATH="$M2_HOME/bin:$PATH"
        GIT_REPO = 'https://github.com/swatigadagi/Demo.git' // Change to your Git repository URL
        DEPLOY_DIR = '/home/ubuntu' // Path to deploy WAR file (e.g., Tomcat webapps directory)
        PORT = '8081' // Port to run the application
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url: "${GIT_REPO}", branch: 'main' // Change branch if necessary
            }
        }
        stage('Build Application') {
            steps {
                script {
                    // Run Maven to build the project
                    sh 'mvn clean package'
                }
            }
        }
        stage('Run Application') {
            steps {
                script {
                    // Run the application
                    sh "java -jar target/hello-world-app-1.0-SNAPSHOT.jar &"
                }
            }
        }
    }
    post {
        success {
            script {
                echo "Application deployed successfully!"
                echo "Access it at http://your-server-ip:${PORT}/hello"
            }
        }
        failure {
            echo "Pipeline failed."
        }
    }
}
