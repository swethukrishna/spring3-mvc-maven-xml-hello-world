pipeline{
	agent{
	label 'slave1'
	}
    stages {
       stage("scm"){
            steps{
                git credentialsId: 'git_credentials', url: 'https://github.com/jmstechhome13/spring3-mvc-maven-xml-hello-world.git'
            }
       }
       stage("build"){
           steps{
           sh 'mvn package'
           }
       }
       
    }
	post {
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "ybmadhu404@gmail.com",
                sendToIndividuals: true])
        }
    }
}
