pipeline {
  agent any
  stages {
    stage('Construyendo la App') {
      steps {
        echo 'Construyendo la App'
        sh 'sh run_build_script.sh'
        slackSend(color: 'good', message: 'Se construyo la App de forma exitosa')
      }
    }

    stage('Prueba de Linux') {
      steps {
        echo 'Realizando la Prueba de Linux'
        sh 'sh run_linux_tests.sh'
        slackSend(color: 'good', message: 'Se ha relizado la prueba de linux de forma exitosa')
      }
    }

    stage('Confirmacion Manual') {
      steps {
        echo 'Esperando por la confirmacion manual'
        input 'Esta todo Ok para desplegar'
        timestamps() {
          echo 'Momento de Confirmacion del Ok Manual'
          slackSend(color: 'good', message: 'Se ha relizado la confirmacion manual de forma exitosa')
        }

      }
    }

    stage('Desplegando en Produccion') {
      steps {
        echo 'Desplegando en Produccion'
        slackSend(color: 'good', message: 'Se ha desplegado en produccion de forma exitosa')
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
      slackSend(color: 'warning', message: 'Se ha generado el archivo JenkinsFile, y se ha realizado el push a GitHub')
    }

    failure {
      slackSend(color: 'danger', message: 'Ha fallado algunos de los pasos del Pipeline')
    }

  }
}