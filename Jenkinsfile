pipeline {
  agent any

  tools {                           // si usas node
    nodejs "Node 18"               // nombre de la instalación de Node configurada en Jenkins
  }

  stages {
    stage('Checkout') {
      steps {
        // Clona tu repo
        checkout scm
      }
    }

    stage('Lint HTML/JS') {
      steps {
        // Podrías instalar htmlhint/eslint globalmente en tu agente
        sh 'npm install -g htmlhint eslint'
        // Valida tu HTML (instalá htmlhint y crea .htmlhintrc si querés)
        sh 'htmlhint index.html'
        // Valida tu JS
        sh 'eslint --max-warnings=0 index.html'
      }
    }

    stage('Tests') {
      steps {
        // Si tuvieras tests, por ejemplo con Jest:
        // sh 'npm install'
        // sh 'npm test'
        echo 'Aquí irían los tests si los tuvieras'
      }
    }

    stage('Archive Artifacts') {
      steps {
        archiveArtifacts artifacts: 'index.html', fingerprint: true
      }
    }
  }

  post {
    success {
      echo '🎉 Build OK'
      // notifySlack('good')  // si configurás Slack
    }
    failure {
      echo '🚨 Falló el build'
      // mail to: 'equipo@dominio.com', subject: "Build fallido: ${env.JOB_NAME}", body: "${env.BUILD_URL}"
    }
  }
}
