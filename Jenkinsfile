pipeline{
    agent any
    stages{

        stage("Build the Java Project"){
            steps{
                //echo
                echo "========executing Build the Java Project========"
                // Shell Script
                sh 'mvn -f pom.xml clean package'
            }
            post{
                success{
                    echo "========A executed successfully========"
                    // archiveArtifacts
                    archiveArtidacts artifacts: '**/*.war'
                }
            }
        }

        stage("Deploy to Staging Environment"){
            steps{
                echo "========Deploy to Staging Environment========"
                // pipeline: build
                build job: 'deployToStage'
            }
        }

        stage('Deploy to Prod Environment'){
            steps{
                echo "========Deploy to Prod Environment========"
                //timeout
                timeout(time:5, unit:'DAYS'){
                    //Pipeline: Input Step
                    input message:'Approve PRODUCTION Deployment!'
                }
                build job: 'deploytoprod'
			}
		}
    }
}