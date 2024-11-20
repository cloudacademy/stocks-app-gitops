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
                            sh "cat ./k8s/stocks_api.yaml"
                            sh "sed -i 's+cloudacademydevops/stocks-api.*+cloudacademydevops/stocks-api:r${DOCKERTAG}+g' ./k8s/stocks_api.yaml"
                            sh "cat ./k8s/stocks_api.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/jenkins-gitops-k8s.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}