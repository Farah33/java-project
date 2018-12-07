properties([pipelineTriggers([githubPush()])])

node('linux') { 
	stage('Unit Tests') {
		git 'https://github.com/Farah33/java-project.git'
		sh 'ant -f test.xml -v'	
		junit "reports/result.xml" 	
		}
	stage ('Build') { 
		sh 'ant -f build.xml -v' 
		}
    stage ('Deploy') {
 		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://khadija-farah/'
       	}
    stage('Report'){	
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '6975a8b3-3c1a-4e79-a7f9-97188dbf4dac', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    // some block 
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
        }
	}
}
