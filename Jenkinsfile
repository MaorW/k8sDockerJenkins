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
            agent {
                docker {
                    image 'node:16.13.1-alpine'
                    reuseNode true // No new workspace will be created, and current workspace from current agent will be mounted into container
                }
            }
            steps {
                sh 'node --version'
            }
             post{
                always{
                    sh 'docker rm ${docker ps -aq}'
                }
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