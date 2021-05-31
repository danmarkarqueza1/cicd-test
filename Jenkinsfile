pipeline {

    agent any

    environment {
        MVNHOME = tool name: 'Maven', type: 'maven'
    }

    stages {

        stage ('Build') {

            steps {
                sh "${MVNHOME}bin/mvn clean package"
            }

        }

        stage ('Deploy') {

            steps {
                         withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                         credentialsId   : 'PCF_LOGIN',
                         usernameVariable: 'USERNAME',
                         passwordVariable: 'PASSWORD']]) {

                    sh '/usr/local/bin/cf login -a https://api.sys.cac.preview.pcf.manulife.com/ -u $USERNAME -p $PASSWORD'
                    sh '/usr/local/bin/cf push'
                }
            }

        }

    }
}