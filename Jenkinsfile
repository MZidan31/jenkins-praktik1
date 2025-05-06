pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Menginstal dependensi...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Menjalankan pengujian...'
                sh 'pytest test_app.py'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Simulating deploy from branch ${env.BRANCH_NAME}"
                // Tambahkan perintah deploy asli jika ada
            }
        }
    }

    post {
        success {
            script {
                def payload = [
                    content: "✅ Build SUCCESS on `${env.BRANCH_NAME}`\n🔗URL: ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: 'https://discordapp.com/api/webhooks/1369293534062182491/yWKUP4CtamVa-9JLWSFH-zLuNqlMZXso3jX5gIhPu3ou7byngUsKux1Mk6H3rbWpAmbS'
                )
            }
        }

        failure {
            script {
                def payload = [
                    content: "❌ Build FAILED on `${env.BRANCH_NAME}`\n🔗URL: ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: 'https://discordapp.com/api/webhooks/1369293534062182491/yWKUP4CtamVa-9JLWSFH-zLuNqlMZXso3jX5gIhPu3ou7byngUsKux1Mk6H3rbWpAmbS'
                )
            }
        }
    }
}