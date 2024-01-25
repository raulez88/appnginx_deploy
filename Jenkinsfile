node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'Github_raulez88', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email raulez88@gmail.com"
                        sh "git config user.name Raulez88"
                        //sh "git switch master"
                        sh "cat nginx-deployment.yaml"
                        sh "sed -i 's/6618959785907.dkr.ecr.eu-west-1.amazonaws.com//nginxcustomimage.*/618959785907.dkr.ecr.eu-west-1.amazonaws.com//nginxcustomimage:${DOCKERTAG}/g' nginx-deployment.yaml"
    
                        sh "cat nginx-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/appnginx_deploy.git HEAD:main"
      }
    }
  }
}
}
