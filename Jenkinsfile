node {
     def app 
     stage('clone repository') {
      checkout scm  
    }
     stage('Build docker Image'){
      app = docker.build("chanderpndy01/chander")
    }
     stage('Test Image'){
       app.inside {
         sh 'echo "TEST PASSED"' 
      }  
    }
     
 
     
     stage('Push Image'){
       docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login') {            
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")   
   }
}
     stage('Remove Unused docker image') {
steps{
sh "docker rmi $app:$BUILD_NUMBER"
sh "docker rmi $app:latest"
sh "docker rmi $app"
}
}
}
