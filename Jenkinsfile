pipeline{
  agent {
    docker { image 'node:8.16.2-alpine3.10' }
  }
  stages{
    stage ('checkout source'){
      steps{
        checkout scm
      }
    }
    stage ('install modules'){
      steps{
        sh '''
          npm install --verbose -d
        '''
      }
    }
    stage ('code quality'){
      steps{
        sh '$(npm bin)/ng lint'
      }
    }
    stage ('build') {
      steps{
        sh '$(npm bin)/ng build --configuration=production'
      }
    }
    // stage ('test'){
    //   steps{
    //     sh '''
    //       $(npm bin)/ng test --watch=false
    //     '''
    //   }
    //   post {
    //       always {
    //         junit "test-results.xml"
    //       }
    //   }
    // }

    stage ('test ui'){
      steps{
        build 'Poc-Automation_Web/master'
      }
    }
  }
}