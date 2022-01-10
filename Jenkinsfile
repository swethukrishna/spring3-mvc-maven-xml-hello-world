pipeline{
    agent any
    stages {
       stage("scm"){
            steps{
                git credentialsId: 'git_credentials', url: 'https://github.com/jmstechhome13/spring3-mvc-maven-xml-hello-world.git'
            }
       }
       stage("build"){
           steps{
           sh 'mvn packagessss'
           }
       }
       
    }
}
