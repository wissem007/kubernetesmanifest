node {
    def app
   environment {
        GITHUB_TOKEN = credentials('jenkins_github')
    }
    
    stage('Cloner le référentiel GitHub') {
            steps {
                git credentialsId: 'jenkins_github', url: 'https://github.com/wissem007/kubernetesmanifest.git'
            }
        }

    stage('Clone repository') {
      

        checkout scm
    }
        
    
        stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'jenkins_github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email alouiwiss@gmail.com"
                        sh "git config user.name wissem007"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+wissem007/kubernetesmanifest.*+wissem007/kubernetesmanifest:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
        
    
    }
