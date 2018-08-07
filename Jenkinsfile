pipeline {
  agent none
  options {
    timeout(time: 15, unit: 'MINUTES')
  }

  stages {
    stage('Builds') {
        parallel {
            stage('Build MacOS') {
              agent {
                label 'xcode'
              }
              when {
                anyOf {
                  branch 'master'
                }
              }
              steps {
                script {
                  sh 'swift build --configuration debug'
                }
              }
            }

            stage('Build Linux') {
              agent any
              when {
                anyOf {
                  branch 'master'
                }
              }
              steps {
                script {
                  mgw.inDocker('liveui/boost-base:1.0') {
                    sh 'swift build --configuration debug'
                  }
                }
              }
            }
        }
    }
  }
}
