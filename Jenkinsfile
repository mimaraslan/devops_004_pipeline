pipeline {
    agent any
    tools {
        maven 'Maven3'
        jdk 'Java21'
    }


    environment {
          APP_NAME = "devops-application"
          RELEASE = "1.0.${env.BUILD_NUMBER}"
          DOCKER_USER = "mimaraslan"
          DOCKER_PASS = 'TOKEN_ID_DOCKER'
          IMAGE_NAME = "${DOCKER_USER}/${APP_NAME}"
          IMAGE_TAG  = "${RELEASE}"

      //    docker build  -t  mimaraslan/devops-application   :  latest     .
    }




    stages {

        stage('Clean Workspace') {
                steps {
                cleanWs()
            }
        }

        stage('SCM GitHub') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mimaraslan/devops_004_pipeline']])
            }
        }

        stage('Build Maven') {
            steps {
                script {
                    if (isUnix()) {
                        sh "mvn clean install"
                    } else {
                        bat "mvn clean install"
                    }
                }
            }
        }


/*
        stage('Test Maven') {
            steps {
                script {
                    if (isUnix()) {
                        sh "mvn test"   // Linux ve MacOS için
                    } else {
                        bat "mvn test"  // Windows için
                    }
                }
            }
        }

        stage('SonarQube') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'TOKEN_ID_SONARQUBE') {
                        if (isUnix()) {
                            sh "mvn sonar:sonar"
                        } else {
                            bat "mvn sonar:sonar"
                        }
                    }
                }
            }
        }
   */




/*
        stage('Docker Image') {
            steps {
                 script {
                    if (isUnix()) {
                        sh 'docker build  -t  mimaraslan/devops-application:latest  .'
                    } else {
                        bat 'docker build  -t  mimaraslan/devops-application:latest  .'
                    }
                }
            }
        }

*/

    stage('Docker Build Image & Push DockerHub') {
            steps {
                 script {
                     docker.withRegistry('', DOCKER_PASS) {
                         myDockerImage  =  docker.build "${IMAGE_NAME}"
                         myDockerImage.push("${IMAGE_TAG}")
                         myDockerImage.push("latest")
                     }
                }
            }
        }



        stage("Trivy Scan") {
            steps {
                script {
                //  docker.withRegistry('', DOCKER_PASS) {
                //        if (isUnix()) {
                            sh ('docker run -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image mimaraslan/devops-application:latest --no-progress --scanners vuln  --exit-code 0 --severity HIGH,CRITICAL --format table')
                //        } else {
                //            bat ('docker run -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image mimaraslan/devops-application:latest --no-progress --scanners vuln  --exit-code 0 --severity HIGH,CRITICAL --format table')
                //        }
                //    }
                }
            }
        }





/*

        stage('DockerHub') {
            steps {
                echo "Image DockerHub'a gönder."
                 script {
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {


                            if (isUnix()) {
                             //   sh 'docker login    -u mimaraslan     -p   %dockerhub%'
                                sh 'docker push mimaraslan/devops-application:latest'
                            } else {
                             //    bat 'docker login    -u mimaraslan     -p   %dockerhub%'
                                 bat 'docker push mimaraslan/devops-application:latest'
                            }
                        }
                 }

            }
        }
*/


// ODEV
/*
   stage('Docker DockerHub') {
            steps {
                 script {
                     docker.withRegistry('', DOCKER_PASS) {
                         docker.build(IMAGE_TAG)
                     }
                }
            }
        }
*/



/*
        stage('Kubernetes (K8s)') {
            steps {
                 script {
                      kubernetesDeploy (configs: 'deployment-service.yaml',  kubeconfigId: 'kubernetes')
                     echo "K8s içinde image'ı çalıştır."
                 }

            }
        }
 */


 /*
       stage('Clean') {
            steps {

                script {
                    if (isUnix()) {
                        sh "docker image prune -f"
                    } else {
                        bat "docker image prune -f"
                    }
                }

            }
        }
 */



        stage('Cleanup Old Docker Images') {
            steps {
                script {
                    if (isUnix()) {
                        // Bu repo için tüm image’leri al, tarihe göre sırala, son 3 hariç sil
                        sh """
                            docker images "${env.IMAGE_NAME}" --format "{{.Repository}}:{{.Tag}} {{.CreatedAt}}" \\
                            | sort -r -k2 \\
                            | tail -n +4 \\
                            | awk '{print \$1}' \\
                            | xargs -r docker rmi -f
                        """

                    } else {
                        bat """
                             for /f "skip=3 tokens=1" %%i in ('docker images ${env.IMAGE_NAME} --format "{{.Repository}}:{{.Tag}}" ^| sort') do docker rmi -f %%i
                        """
                    }
                }
            }
        }





    }
}