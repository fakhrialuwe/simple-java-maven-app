pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh '/opt/apache-maven-3.9.6/bin/mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh '/opt/apache-maven-3.9.6/bin/mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
          steps {
                sh 'export MAVEN_HOME=/opt/apache-maven-3.9.6;export M2_HOME=$MAVEN_HOME;export PATH=$MAVEN_HOME/bin:$PATH;./jenkins/scripts/deliver.sh'
            }
        }
    }
}
