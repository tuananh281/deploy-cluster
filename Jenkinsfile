pipeline {
    agent any
    stages {
        
        stage('Update git') {
            steps {
                script {
                    catchError(buildResult: 'SUCCEESS', stageResult: 'FAILUE'){
                        withCredentials([usernamePassword(credentialsId: 'tuananh_github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]){
                            sh "cat deployment.yaml"
                            sh "sed -i s+tuannanhh/train-schedule:*+tuannanhh/train-schedule:${DOCKERTAG}+g" deployment.yaml
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done get changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://github.com/tuananh281/cicd-pipeline-train-schedule-dockerdeploy.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
