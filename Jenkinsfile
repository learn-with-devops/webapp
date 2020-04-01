#!groovy

pipeline{

	agent any

	stages{

		stage ('clening the workspace'){

			steps{

				echo "Deleting the workspace"
				deleteDir()
			}
		}

		stage ('Checkout the latest code'){

			steps{
			
				echo "Downloding the code from github"
				checkout scm
			}
		}

		stage ('Compiling the code'){

			steps{
			
				script{

					echo "Compiling the code"
					sh 'mvn compile'
				}
			}
		}

		stage ('Packaging the code'){

			steps{
			
				script{

					echo "Package the code"
					sh 'mvn package'
				}
			}
		}

		stage ('Deploy the code'){

			steps{
			
				script{

					echo "Deploying  the code"
					sh 'sudo sh /root/application_deployment.sh'
				}
			}
		}
	}
}
