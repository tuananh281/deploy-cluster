pipeline {
    agent any
    stages {       
        stage('Update git') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                        withCredentials([usernamePassword(credentialsId: 'tuananh_github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]){
                        // withCredentials([usernamePassword(credentialsId: 'tuananh_github')]){
                            sh "cat deployment.yaml"
                            sh "sed -i 's+tuannanhh/train-schedule:*+tuannanhh/train-schedule:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done get : ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/deploy-cluster.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
