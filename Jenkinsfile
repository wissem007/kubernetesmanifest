node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'jenkinstogithub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email alouiwiss@gmail.com"
                        sh "git config user.name wissem007"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+wissem007/python.*+wissem007/python:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${USERNAME}:${PASSWORD}@github.com/${USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
