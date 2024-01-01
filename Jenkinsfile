pipeline{
    agent any
    tools { 
        maven 'maven' 
        docker 'docker' 
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
           steps{
               dir("cicd"){
                    sh " ls -al"
                    sh " docker build . sample:latest"
                    sh "docker tag sample:latest zhuwj726/tc:latest"
                    sh "docker push zhuwj726/tc:latest"
                }
           }
       }

    }
}
