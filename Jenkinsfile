pipeline {
    agent any
    environment {
		STAGINGSERVER = '178.128.223.0'
	}
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build'
                archiveArtifacts artifacts: 'src/index.html'
            }
        }
        stage('DeployToStage') {
            //when {
            //    branch 'master'
            //}
            steps {
                sh 'scp -r src/* deployer@$STAGINGSERVER:/home/deployer/staging/html/'
            }

        }
        stage('DeployToProd') {
            //when {
            //    branch 'master'
            //}
            steps {
                input message: 'Yakin mau deploy ?', ok: 'Yakin'
                milestone(1)
                sh 'scp -r src/* deployer@$STAGINGSERVER:/home/deployer/production/html/'
            }
        }
    }
}
