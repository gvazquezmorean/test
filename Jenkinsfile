pipeline {
  agent any
  stages {

    stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      //   git branch: 'main', url: 'https://github.com/hardeepsonatype/zippedtest.git', skipTag: true, shallow: true
      steps {
        git branch: 'main', url: 'https://github.com/gvazquezmorean/test'
      }

    }
    stage('Build') {
      tools {
        jdk 'JAVA11'
        maven 'MAVEN3.9.9'
      }
      steps {

        sh 'java -version'
        // sh 'mvn -B -DskipTests clean package'                 
        sh 'mvn -B clean install dependency:copy-dependencies'

        nexusPolicyEvaluation iqStage: 'build', iqApplication: 'testapp', iqInstanceId: 'local',
          //el de abajo funcionando con mis cambios
          //iqScanPatterns: [[scanPattern: '**'], [scanPattern: '!*.zip']]
          //iqScanPatterns: [[scanPattern: '**'], [scanPattern: ' '], [scanPattern: '!*.zip']]
          //el de abajo funcionando con mis cambios
          //iqScanPatterns: [[scanPattern: '**'], [scanPattern: '!*.zip'], [scanPattern: '!dependance2/**']] 
          //el de abajo funcionando con mis cambios
          //iqScanPatterns: [[scanPattern: '**'], [scanPattern: '!/*.zip']]
          //iqScanPatterns: [[scanPattern: '**'], [scanPattern: '!dependance2/**']] 

          //iqScanPatterns: [[scanPattern: '**'], [scanPattern: '!dependance2/xstream-1.4.5.jar']]
          // el de abajo NO funciona con mis cambios, no me trae nada asi
          //iqScanPatterns: [[scanPattern: '**'], [scanPattern: '!*.zip']]
          // el de abajo funcionando con mis cambios
          //iqScanPatterns: [ [scanPattern: '**'], [scanPattern: '!/*.zip']] 
          iqScanPatterns: [
            [scanPattern: '**'],
            [scanPattern: '!*.zip']
          ],
          failBuildOnNetworkError: true,
          callflow: [
            enable: true
          ]
      }

    }
  }
}
