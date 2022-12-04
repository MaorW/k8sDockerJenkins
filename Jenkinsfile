pipeline{
    agent{
        agent any
    }
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
    }
}