pipeline{
    agent any
    stages{
        stage("Build the Java Project"){
            steps{
                echo "========executing Build the Java Project========"
                sh 'mvn -f pom.xml clean package'
            }
            post{
                success{
                    echo "========A executed successfully========"
                    archiveArtidacts artifacts: '**/*.war'
                }
            }
        }

        stage("Deploy to Staging Environment"){
            steps{
                echo "========Deploy to Staging Environment========"
                build job: 'deployToStage'
            }
        }

        stage('Deploy to Prod Environment'){
				steps{
                    echo "========Deploy to Prod Environment========"
					timeout(time:5, unit:'DAYS'){
					input message:'Approve PRODUCTION Deployment!'
				}
				build job: 'deploytoprod'
			}
		}

    }
}