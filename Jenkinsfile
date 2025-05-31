pipeline {
    agent any

    stages {
        stage('Install Packages') {
            steps {
                sh '''
                    sudo apt update -y
                    sudo apt install -y openjdk-11-jdk maven git wget
                '''
            }
        }

        stage('Clone Repository') {
            steps {
                git 'https://github.com/SunilB565/Train-Ticket-Reservation-System.git'
            }
        }

        stage('Download and Extract Tomcat') {
            steps {
                sh '''
                    wget https://dlcdn.apache.org/tomcat/tomcat-11/v11.0.7/bin/apache-tomcat-11.0.7.tar.gz
                    tar -xzvf apache-tomcat-11.0.7.tar.gz
                    rm -f apache-tomcat-11.0.7.tar.gz
                '''
            }
        }

        stage('Build Project') {
            steps {
                sh '''
                    cd Train-Ticket-Reservation-System
                    mvn clean install
                '''
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                sh '''
                    cp Train-Ticket-Reservation-System/target/TrainBook-1.0.0-SNAPSHOT.war apache-tomcat-11.0.7/webapps/
                    cd apache-tomcat-11.0.7/webapps
                    rm -rf ROOT
                    mv TrainBook-1.0.0-SNAPSHOT.war ROOT.war
                '''
            }
        }

        stage('Start Tomcat Server') {
            steps {
                sh '''
                    cd apache-tomcat-11.0.7/bin
                    chmod +x *.sh
                    ./startup.sh
                '''
            }
        }
    }
}
