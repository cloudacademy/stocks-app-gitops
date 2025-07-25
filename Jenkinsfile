pipeline {
    agent any

    stages {
        stage('GitOps - Manifest Update') {
            steps {
                script {
                    if (IMAGE == 'cloudacademydevops/stocks-app-jdemo') {
                        echo 'stocks-app-jdemo: patching manifest file...'
                        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                            withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                                sh "git config user.name Jeremy Cook"
                                sh "git config user.email jeremy.cook@qa.com"
                                sh "ls -la"
                                sh "echo TAG: ${TAG}"
                                sh "cd k8s && sed -i 's+\\(cloudacademydevops/stocks-app-jdemo:\\).*+\\1${TAG}+g' 3_stocks_app.yaml"
                                sh "git add ."
                                sh "git commit -m 'jenkins build changemanifest: ${env.BUILD_NUMBER}'"
                                sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/cloudacademy/stocks-app-gitops.git HEAD:jenkins-demo"
                            }
                        }
                    } else if (IMAGE == 'cloudacademydevops/stocks-api-jdemo') {
                        echo 'stocks-api-jdemo: patching manifest file...'
                        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                            withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                                sh "git config user.name Jeremy Cook"
                                sh "git config user.email jeremy.cook@qa.com"
                                sh "ls -la"
                                sh "echo TAG: ${TAG}"
                                sh "cd k8s && sed -i 's+\\(cloudacademydevops/stocks-api-jdemo:\\).*+\\1${TAG}+g' 2_stocks_api.yaml"
                                sh "git add ."
                                sh "git commit -m 'jenkins build changemanifest: ${env.BUILD_NUMBER}'"
                                sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/cloudacademy/stocks-app-gitops.git HEAD:jenkins-demo"
                            }
                        }
                    }
                }
            }
        }
    }
}