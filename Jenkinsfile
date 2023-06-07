pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "mvn compile"
               }
          }
          stage("Unit test") {
               steps {
                    sh "mvn test"
               }
          }
     
    
stage("Package") {
     steps {
          sh "mvn package"
     }
}
stage("Docker build") {
     steps {
      
          sh "docker build -t deepak_tomcat ."
     }
}

stage("Deploy to staging") {
     steps {
          
          sh "docker stop \$(docker ps -qa)"
          sh "docker rm \$(docker ps -qa)"
          sh "docker run -d -it -v /root/.jenkins/workspace/tomcat-docker-pipeline/target/:/usr/local/tomcat/webapps/ -p 8081:8080 --name Testtomcat deepak_tomcat"
     }
}

     }
  post {
     always {
          sh "echo 'I did It'"
     }
}
}
