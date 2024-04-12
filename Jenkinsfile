node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email ashith.ss@gmail.com"
                    sh "git config user.name ashith.ss"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+ashithss/packages.*+ashithss/packages:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'By Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@gitlab.10.16.85.156.nip.io/devops-solutions/k8s-github-pilot.git HEAD:main" 
                }
            }
        }
    }
}