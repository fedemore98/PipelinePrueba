pipeline {
  agent any
  stages {
    stage('Construyendo la App') {
      steps {
        echo 'Construyendo la App'
        sh 'sh run_build_script.sh  '
      }
    }

    stage('Prueba de Linux') {
      steps {
        echo 'Realizando la Prueba de Linux'
        sh 'sh run_linux_tests.sh'
      }
    }

    stage('Confirmacion Manual') {
      steps {
        echo 'Esperando por la confirmacion manual'
        input 'Esta todo Ok para desplegar'
        timestamps() {
          echo 'Momento de Confirmacion del Ok Manual'
        }

      }
    }

    stage('Desplegando en Produccion') {
      steps {
        echo 'Desplegando en Produccion'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
      slackSend(message: 'Message from Jenkins Pipeline')
      slackSend(message: 'Message from Jenkins Pipeline2')
    }

  }
}