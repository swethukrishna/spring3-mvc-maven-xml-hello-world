pipeline {
   agent any
   environment 
    {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'javaapp'
        IMAGE = "$PROJECT:$VERSION"
        ECRURL = 'https://041221872505.dkr.ecr.ap-south-1.amazonaws.com'
        ECRCRED = 'ecr:ap-south-1:awscredentials'
    }   
    stages {
      stage('GetSCM') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/jmstechhome13/spring3-mvc-maven-xml-hello-world.git'
         }
         }
     stage('build') {
         steps {
          sh 'mvn package'
         }
         }
     stage('Image Build'){
             steps{
                 script{
                       sh 'docker build -t ${IMAGE} .'
                 }
             }
         }
      stage('Push Image'){
         steps{
             script
                {
                   
                    docker.withRegistry(ECRURL, ECRCRED)
                    {
                        docker.image(IMAGE).push()
                    }
                }
            }
         }

     stage('deploymnet'){
         steps{
             sh 'sudo ansible-playbook deployment_object.yaml -i deploy --extra-vars "version=$VERSION"'
            }
         }   
   
}
}
