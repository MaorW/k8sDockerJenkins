pipeline{
    agent any
    stages{
        stage("Cloning ..."){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/MaorW/k8sDockerJenkins.git']]])
            }
            post{
                success{
                    echo "The repo has been cloned successfully ..."
                }
                failure{
                
                    mail to: 'learningmw1991@gmail.com',
                        subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                        body: "Something is wrong with ${env.BUILD_URL}"
                }
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t learningmw1991/simple_react_js_project:01 ./kub'
            }
             post{
                success{
                    echo "The build has been run successfully ..."
                }
                failure{
                    mail to: 'learningmw1991@gmail.com',
                        subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                        body: "Something is wrong with ${env.BUILD_URL}"
                }
            }
        }
    }
}