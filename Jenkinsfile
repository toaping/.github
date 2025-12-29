pipeline {
    agent any

    stages {
        stage('Source Checkout') {
            steps {
                // Github에서 코드를 가져옵니다.
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building Application...'
                // 여기에 실제 빌드 명령어(예: sh 'npm install')를 넣습니다.
            }
        }
    }

    // 빌드 결과에 따른 Slack 알림
    post {
        always {
            script {
                def buildStatus = currentBuild.currentResult // SUCCESS, FAILURE 등
                def color = (buildStatus == 'SUCCESS') ? '#00FF00' : '#FF0000'
                
                slackSend (
                    channel: '#소셜', // 본인의 채널명
                    color: color,
                    message: "📢 *Build ${buildStatus}*: Job '${env.JOB_NAME}' [#${env.BUILD_NUMBER}]\nCheck it out here: ${env.BUILD_URL}"
                )
            }
        }
    }
}
