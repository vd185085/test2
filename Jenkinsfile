#!groovy

pipeline {

  agent any

  options {

    buildDiscarder(
      logRotator(numToKeepStr: '5')
    )

    disableConcurrentBuilds()

    timeout(time: 20, unit: 'MINUTES') 

  }

  stages {

    stage('Build') {

      steps {

        script {

          def nantBuildStatus = bat(
            label: 'Run nant build to build the project',
            returnuStatus: true,
            script: 'nant -buildfile:andc.build code-build'
          )

          if (nantBuildStatus != 0) {
            println "status returned by nantBuildStatus :: ${nantBuildStatus}"
            error "Unable to build project using 'nant -buildfile:andc.build code-build' please check"
          }

        }

      }

    }

  }

  post {

    success {

      println "Job 'Auto trigger-AANDC-CPP' has been completed Successfully"

    }

    unsuccessful {

      println "Job 'Auto trigger-AANDC-CPP' has been failed due to an error"

    }

  }

}
