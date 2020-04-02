#!groovy

def branch

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
				script{
					branch = env.BRANCH_NAME
					echo "The current branch is ${branch}"
				}
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

		stage ('Deploy the code in to Dev'){

			when {
                expression { branch == 'dev'}
               }
            steps{
                script{

                    echo "Dev code is deploying"
                    sh 'sudo sh /root/dev_branch.sh'
                    }
                }
		}

		stage ('Deploy the code in to QA'){

			when {
                expression { branch == 'qa'}
               }
            steps{
                script{

                    echo "Dev code is deploying"
                    sh 'sudo sh /root/qa_branch.sh'
                    }
                }
		}

		stage ('Deploy the code in to Master'){

			when {
                expression { branch == 'master'}
               }
            steps{
                script{

                    echo "Dev code is deploying"
                    sh 'sudo sh /root/master_branch.sh'
                    }
                }
		}
		
	    stage('Finally Calling Other Job')
	          {
		steps {
			build job: 'testing_job', quietPeriod: 0
		}
	}
	}
}
