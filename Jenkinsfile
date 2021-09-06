pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                git branch: 'Grupa03-KM306474_Popr_Lab07-10', url: 'https://github.com/InzynieriaOprogramowaniaAGH/MIFT2021'
                dir('Grupy/Grupa03/KM306474/Popr_Lab07-10/Build'){
                    
                    sh '''
                        curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o ~/docker-compose
                        chmod +x ~/docker-compose
                        ~/docker-compose up
                        ls -l
                        docker --version
                    ''' 
                }

            }
            post
			{
				failure
				{
					echo 'Build failed'
					emailext attachLog: true,
						body: "Status: ${currentBuild.currentResult}",
						recipientProviders: [[$class: 'DevelopersRecipientProvider']],
						subject: 'Building has  failed',
						to: 'krzysztofmarcinek98@gmail.com'
				}
				success
				{
					echo 'Build success'
				}
			}
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            
                git branch: 'Grupa03-KM306474_Popr_Lab07-10', url: 'https://github.com/InzynieriaOprogramowaniaAGH/MIFT2021'
                dir('Grupy/Grupa03/KM306474/Popr_Lab07-10/Test'){
                    
                    sh '''
                        ~/docker-compose up
                    ''' 

                }
            }
        }
    }
        post{
            success {
                emailext attachLog: true,
                    to: 'krzysztofmarcinek98@gmail.com',
                    subject: "Success ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                    body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}"
            }
            failure {
                emailext attachLog: true,
                    to: 'krzysztofmarcinek98@gmail.com',
                    subject: "Failed  ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                    body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}"
            }
        }
        stage('Deploy') {
                steps {
                    echo 'Deploying...'
                    git branch: 'Grupa03-KM306474_Popr_Lab07-10', url: 'https://github.com/InzynieriaOprogramowaniaAGH/MIFT2021'
                    dir('Grupy/Grupa03/KM306474/Popr_Lab07-10/Deploy'){
                       sh 'docker build --no-cache -t tetris_deploy .'
                    }
                }
                post
                {
                    failure {
                        echo 'Deployment has failed'
                        emailext attachLog: true,
                            body: "Status: ${currentBuild.currentResult}",
                            subject: 'Deployment has failed',
                            to: 'krzysztofmarcinek98@gmail.com'
                    }
                    success {
                        echo 'Deployment success'
                    }
                }
            }
        }
        post {
            success {
                echo 'Jenkins Success'
                emailext attachLog: true,
                        body: "Status: ${currentBuild.currentResult}",
                        subject: 'Jenkins completed',
                        to: 'krzysztofmarcinek98@gmail.com'
            }
            failure {
                echo 'Jenkins Faild'
                emailext attachLog: true,
                        body: "Status: ${currentBuild.currentResult}",
                        subject: 'Jenkins failed',
                        to: 'krzysztofmarcinek98@gmail.com'
            }
        }
}