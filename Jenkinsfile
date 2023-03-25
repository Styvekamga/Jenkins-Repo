pipeline {
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven-3.0.5/bin"
    }

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
                dir('/var/lib/jenkins/workspace/New_demo')
                {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        
        stage('SonarQube analysis') {
            steps {
               withSonarQubeEnv('sonarqube-8.9.7')
                {
                    //sh "${scannerHome}/bin/sonar-scanner"
                    sh "mvn sonar:sonar"
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
