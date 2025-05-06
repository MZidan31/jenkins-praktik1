pipeline {
    agent {
        docker {
            image 'python:3.11' // Gunakan image resmi Python dari Docker Hub
            args '-u root'      // Menjalankan container sebagai root (opsional)
        }
    }

    environment {
        DISCORD_WEBHOOK = 'https://discordapp.com/api/webhooks/1369293534062182491/yWKUP4CtamVa-9JLWSFH-zLuNqlMZXso3jX5gIhPu3ou7byngUsKux1Mk6H3rbWpAmbS'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo '🔧 Menginstal dependensi...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Menjalankan pengujian...'
                sh 'pytest test_app.py'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "🚀 Simulating deploy dari branch ${env.BRANCH_NAME}"
                // Tambahkan perintah deploy asli jika ada
            }
        }
    }

    post {
        success {
            script {
                def payload = [
                    content: "✅ Build SUCCESS on `${env.BRANCH_NAME}`\n🔗 ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: "${DISCORD_WEBHOOK}"
                )
            }
        }

        failure {
            script {
                def payload = [
                    content: "❌ Build FAILED on `${env.BRANCH_NAME}`\n🔗 ${env.BUILD_URL}"
                ]
                httpRequest(
                    httpMode: 'POST',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload),
                    url: "${DISCORD_WEBHOOK}"
                )
            }
        }
    }
}
