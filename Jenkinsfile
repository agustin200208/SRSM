pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Clona tu repo
        checkout scm
      }
    }

    stage('Validar HTML (opcional)') {
      steps {
        echo '🔍 Validando index.html'
        // Si tienes instalado `tidy`, descomenta la línea:
        // sh 'tidy -q -e index.html || true'
      }
    }

    stage('Archive Artifact') {
      steps {
        // Guarda tu index.html como artefacto
        archiveArtifacts artifacts: 'index.html', fingerprint: true
      }
    }
  }

  post {
    success {
      echo '✅ Build exitoso: tu HTML está en orden'
    }
    failure {
      echo '❌ Build fallido'
    }
  }
}
