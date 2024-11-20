pipeline {
    agent any

    stages {
        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            sh "git config user.name Jeremy Cook"
                            sh "git config user.email jeremy.cook@qa.com"
                            sh "ls -la"
                            sh "echo DOCKERTAG: ${DOCKERTAG}"
                            sh "cd k8s && sed -i 's+\\(cloudacademydevops/stocks-api:\\).*+\\1${DOCKERTAG}+g' 2_stocks_api.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/cloudacademy/stocks-app-gitops.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}