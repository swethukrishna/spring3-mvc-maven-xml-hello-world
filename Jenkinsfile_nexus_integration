 pipeline{
    agent any
      tools {
        maven "maven3"
    }
    stages{
        stage("scm"){
            steps{
               git credentialsId: 'github_credentials', url: 'https://github.com/jmstechhome13/spring3-mvc-maven-xml-hello-world.git'            }
        }
        stage("build"){
            steps{
              sh 'mvn package'        
              }
        }
        stage("artifact"){
            steps{
           archiveArtifacts artifacts: 'target/*.war'
           }
        }
      	stage('deploy') {
             steps{
                 withCredentials([usernameColonPassword(credentialsId: 'remote_tomcat_credentails', variable: 'tomcatcred')]) {
                                      sh "curl -v -u $tomcatcred -T /var/lib/jenkins/workspace/git-maven/target/spring3-mvc-maven-xml-hello-world-1.0-SNAPSHOT.war 'http://ec2-65-0-72-74.ap-south-1.compute.amazonaws.com:8080/manager/text/deploy?path=/tomcat-pipeline&update=true'"
                    }
                
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
                recipients: "ybmadhuit@gmail.com,divyapathakota@gmail.com,kasi.umamaheswari7@gmail.com,Vasudhareddy87@gmajl.com",
                sendToIndividuals: true])
        }
    }
 } 
 
