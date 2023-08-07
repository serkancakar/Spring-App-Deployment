node {
    def app

    stage('Clone repository') {


        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email halilserkancakar.com"
                        sh "git config user.name serkancakar"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+harbor.tmc.datamarket.local/app/spring-app.*+harbor.tmc.datamarket.local/app/spring-app:${BUILD_NUMBER}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Spring-App-Deployment.git HEAD:main"
      }
    }
  }
}
}
