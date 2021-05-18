pipeline{
    agent any
    environment{
	dockerimage = ''
	registryCredentails = 'rajat2509'
	registry = 'rajat2509/jenkins-docker-jar-image'
        PATH= "/opt/maven3/bin:$PATH"
    }
        stages {
            stage('git'){
                steps{
                    
                    echo 'Pulling Git Repository' 
                    git branch: 'master',url:'https://github.com/rajat990/jar-image.git', credentialsId: 'a2710884-80a9-451b-bd36-57a5882822fc'
                    
                }
            }
          
      stage('docker-image-build'){
	steps{
		script {
			dockerimage = docker.build registry
			}
		}
	}
    stage('docker-image-upload'){
      steps{
        script{
         docker.withRegistry( '', registryCredentails ){

         dockerimage.push()}
        }
      }
    }
    stage('Clea/ning up') {
        steps{
    
   
        bat 'docker images'
        bat 'docker ps -a'
    //     bat 'docker images'
    //     bat 'docker ps -a'
        }
    }
    stage('pull image from docker hub') {
        steps{
        bat "docker pull $registry"
        
        bat 'docker images -a'
        bat 'docker ps -a'
        
        }
    }
    stage('run image at 8080 port') {
        steps{
        bat "docker run -p 8080:8080 $registry"
        }
    }
   
        }
    
}