pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                    export MAVEN_HOME=/usr/local/Cellar/maven/3.6.1
                    export PATH=$PATH:$MAVEN_HOME/bin
                    sh 'mvn clean package'
            }
        }

        stage ('Deploy') {
            steps {

                withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                                  credentialsId   : 'PCF_LOGIN',
                                  usernameVariable: 'USERNAME',
                                  passwordVariable: 'PASSWORD']]) {

                    sh '/usr/local/bin/cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                    sh '/usr/local/bin/cf push'
                }
            }

        }

    }

}
