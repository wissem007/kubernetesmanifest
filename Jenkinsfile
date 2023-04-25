node {
    def app
   environment {
        GITHUB_TOKEN = credentials('jenkins_github')
    }

    stage('Clone repository') {
      

        checkout scm
    }
        
        
        
     stage('Mettre à jour le fichier') {
            steps {
                sh "cat deployment.yaml"
                sh "sed -i 's+wissem007/python.*+wissem007/python:${DOCKERTAG}+g' deployment.yaml"
                sh "cat deployment.yaml"
                sh "git add ."

                sh 'echo "Nouveau contenu" > fichier_a_modifier.txt'
                sh 'git add fichier_a_modifier.txt'
                sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
            
                sh 'git push origin main'
            }
        }
    }
