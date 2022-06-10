pipeline{
    agent{
        label 'docker'
    }
    options{ timestamps() }
    
    stages{
        parallel{
            stage('chrome-last'){
                agent{
                    node{
                        label "docker"
                        customWorkspace "workspace/chrome-last"
                        }
                    }
            steps{
                script{
                    sh "docker build -t chrome-last --target chrome_last ."
                    sh "cd $WORKSPACE"
                    sh "docker run --rm --shm-size='4g' chrome-last --browser chrome --headless -n 2 --alluredir=allure-results"
                }
            }
            post{
                always{
                    allure([
                        reportBuildPolicy: 'ALWAYS',
                        results: [[path: './allure-results']]
                    ])
                }
            }
        }
            stage('firefox-last'){
                    agent{
                        node{
                            label "docker"
                            customWorkspace "workspace/firefox-last"
                            }
                        }
                steps{
                    script{
                        sh "docker build -t firefox-last --target firefox_last ."
                        sh "cd $WORKSPACE"
                        sh "docker run --rm --shm-size='4g' firefox-last --browser firefox --headless -n 2 --alluredir=allure-results"
                    }
                }
                post{
                    always{
                        allure([
                            reportBuildPolicy: 'ALWAYS',
                            results: [[path: './allure-results']]
                        ])
                    }
                }
            }
        }
    }
}
        

