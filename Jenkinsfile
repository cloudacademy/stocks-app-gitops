pipeline {
    agent any

    stages {
        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                            sh "git config user.name Jeremy Cook"
                            sh "git config user.email jeremy.cook@qa.com"
                            //sh "git switch master"
                            sh "ls -la"
                            sh "echo DOCKERTAG: ${DOCKERTAG}"
                            sh "cd k8s && sed -i 's+cloudacademydevops/stocks-api.*+cloudacademydevops/stocks-api:r${DOCKERTAG}+g' 2_stocks_api.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/cloudacademy/jenkins-gitops-k8s.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}