pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                export M2_HOME=/usr/local/Cellar/maven/3.6.1 # your Mavan home path
                export PATH=$PATH:$M2_HOME/bin
                    sh 'mvn -v'
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
