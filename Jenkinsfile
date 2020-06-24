pipeline {
    agent any

	tools {
		maven 'Maven3.6'
		jdk 'JDK1/8'
	}
//
//	environment {
//		M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				print "Deployment is done!"
				sh 'sshpass -p "gamut" scp target/gamutkart.war gamut@172.17.0.3:/home/gamut/apache-tomcat-7.0.104/webapps'
				sh 'sshpass -p "gamut" ssh -o StrictHostKeyChecking=no gamut@172.17.0.3 "JAVA_HOME=/usr/bin/java" "/home/gamut/apache-tomcat-7.0.104/bin/startup.sh"'	


	    	}
		}
    }
}
