pipeline {
    agent any

    stages {
        stage('pull code') {
            steps {
                git branch: 'webdemo', credentialsId: 'e33ee91a-d570-412a-80dc-88b0f6d2562f', url: 'git@github.com:xlqywk/webdemo.git'
            }
        }
        stage('build') {
            steps {
                sh '''/usr/local/sbin/mvn clean package'''
            }
        }
        stage('publish') {
            steps {
                sh '''export BUILD_ID=dontKillMe
                    source /etc/profile
                    bash /data/scripts/cicd.sh'''
            }
        }
    }
        post {
              always{
                    emailext(
                      body: '${FILE,path="email.html"}',
                      subject: '构建通知：${PROJECT_NAME}',
                      to: '48211701@qq.com'
                    )
                }
        }
}

