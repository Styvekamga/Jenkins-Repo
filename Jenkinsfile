pipeline {
    agent any

    tools {
        maven "M2_HOME"
        jdk "JAVA_HOME"
    }

    stages {
        stage('Initialize') {
            steps {
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
       stage('Checkout SCM') {
   steps {
       git branch: 'main', url: 'https://github.com/Styvekamga/Jenkins-Repo.git'
   }
}
        stage('Build') {
            steps {
                dir('/var/lib/jenkins/workspace/New_demo/my-app')
                {
                    sh 'mvn generate-pom'
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
    }
    post {
        always {
            junit(
                allowEmptyResults: true,
                testResults: '**/target/surefire-reports/*.xml'
            )
        }
    }
}
