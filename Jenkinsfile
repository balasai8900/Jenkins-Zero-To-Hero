pipeline {
    agent any

    environment {
        imagename = "sysmaster/sysmasterapp-${env.BUILD_ID}"
       // registryCredential = 'GitLab_Credentials_369258'
        dockerImage = ''
        registryUrl = 'http://3.108.56.62'  // Replace with your Docker registry IP address
    }

    stages {
        stage('Cloning Git') {
            steps {
                git(
                    url: 'https://github.com/balasai8900/Jenkins-Zero-To-Hero.git',
                    branch: 'main',
                    // credentialsId: 'GitLab_Credentials_369258'
                )
            }
        }

      // stage('Maven Build') {
         //   steps {
           //     script {
                    // Add Maven build command here
             //       sh 'mvn clean install'
               // }
      //      }
        //}

        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build(imagename)
                }
            }
        }
  
  stage('Run Docker Container') {
            steps {
                script {
                // Run the Docker container
                //sh "docker run -d --name sysmasterapp:$CI_PIPELINE_ID -p 9025:9025 sysmaster/sysmasterapp:latest"
                // Define the container name
                def containerName = "sysmasterapp-${env.BUILD_ID}"

                // Stop and remove the old container if it exists
                sh "docker rm -f ${containerName} || true"

                    // Run the Docker container
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        sh "docker run -d --name ${containerName} -p 9025:9025 ${imagename}:latest"
                    }
                }
            }
        }
    }
}
