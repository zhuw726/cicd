pipeline{
    agent any
    tools { 
        maven 'maven' 
    }
    stages{
        stage("Clean up"){
            steps{
                 sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                    mvn -version
                ''' 
                deleteDir()
            }
        }
        stage("clone repo"){
            steps{
                sh "git clone https://github.com/zhuw726/cicd.git"
            }
        }
        stage("build"){
            steps{
                dir("cicd"){
                    sh "mvn clean install"
                }
            }
        }
        stage("test"){
            steps{
                dir("cicd"){
                    sh "mvn test"
                }
            }
        }
       stage("build & push docker hub"){
            // agent {
            //     docker { image 'maven:3.9.6-eclipse-temurin-17-alpine' }
            // }
           steps{
            // script {
            //         def dockerHome = tool 'docker'
            //         env.PATH = "${dockerHome}/bin:${env.PATH}"
            // }
            agent {
                docker { image 'docker:24.0.5' }
            }
               dir("cicd"){
                    // sh " def dockerHome = tool 'docker'"
                    // sh " env.PATH = '${dockerHome}/bin:${env.PATH}'"
                    sh "ls -al"
                    sh "docker build . -t sample:latest"
                    sh "docker tag sample:latest zhuwj726/tc:latest"
                    sh "docker push zhuwj726/tc:latest"
                }
           }
       }

    }
}
